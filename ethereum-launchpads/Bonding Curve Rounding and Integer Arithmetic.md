---
topic: Bonding Curve Rounding and Integer Arithmetic
type: concept
tags: [bonding-curve, integer-arithmetic, rounding, solidity, pool-solvency, uniswap, defi-math]
confidence: high
last_updated: 2026-04-02
sources:
  - https://github.com/Uniswap/v2-periphery/blob/master/contracts/libraries/UniswapV2Library.sol
  - https://github.com/adshao/publications/blob/master/uniswap/dive-into-uniswap-v2-contracts/README.md
  - https://uniswapv3book.com/milestone_4/tick-rounding.html
  - https://docs.uniswap.org/contracts/v4/concepts/hooks
---

## Summary
Bonding curves and AMM pools operate on integer (uint256) arithmetic — there are no floating-point numbers in the EVM. Rounding decisions are not neutral: they can drain pool reserves over time or leave dust stuck in contracts. The canonical rule across DeFi is "round against the trader" — tokens out rounds down, tokens in rounds up — to protect pool solvency.

## Key Facts

### Why Rounding Matters
- EVM arithmetic is integer-only; division truncates toward zero (floor division)
- Every swap involves at least one division, introducing a rounding error of up to 1 wei per operation
- Over millions of swaps, systematic rounding in the wrong direction can accumulate into pool insolvency
- Conversely, rounding always in the pool's favour creates dust accumulation and prevents exact token amounts from being withdrawn

> [!fact] Pool solvency invariant: after every swap, the pool's invariant (e.g., x * y = k) must not decrease. Rounding that favours traders can violate this invariant over time.

### Uniswap V2: Round Against Trader
- `getAmountOut(amountIn, reserveIn, reserveOut)`: computes tokens_out using integer division — naturally rounds **down** (fewer tokens out)
- `getAmountIn(amountOut, reserveIn, reserveOut)`: computes tokens_in needed for a desired output — adds `+1` explicitly to round **up** (more tokens in required)
- The `+1` in `getAmountIn` is a deliberate rounding correction:
  ```solidity
  // From UniswapV2Library.sol
  amountIn = (reserveIn * amountOut * 1000) / ((reserveOut - amountOut) * 997) + 1;
  ```
- Fee calculation: instead of multiplying by `0.997` (0.3% fee), V2 multiplies by `997` and divides by `1000` — avoids decimal issues entirely
- Result: integer arithmetic with explicit rounding corrections keeps the `k` invariant always satisfied or growing

> [!fact] The `+ 1` in UniswapV2Library.sol getAmountIn is confirmed from source code — it explicitly rounds the required input amount up to protect pool solvency.

### Uniswap V3: Asymmetric Rounding Favouring Pool
- V3 introduces **tick-based concentrated liquidity** — prices are discrete, mapped to tick indices
- Tick rounding: when a user specifies an off-tick price, the SDK rounds to the **nearest usable tick** via `nearestUsableTick()`
- For swaps: `amounts out` round down, `amounts in` round up — same principle as V2
- Additional V3 consideration: **sqrtPrice** (stored as Q64.96 fixed-point) introduces precision loss at the root computation step
- V3 uses Q notation (binary fixed-point) rather than scaling by 1000 — higher precision but same directional rounding
- Cross-tick swaps accumulate multiple rounding steps; the directional invariant is maintained at each step

> [!analysis] V3's increased complexity (tick math, sqrtPrice, Q64.96) creates more opportunities for subtle rounding bugs. Multiple audits have found edge cases where accumulated rounding in tick transitions could create tiny insolvencies.

### Uniswap V4: Customizable via Hooks
- V4 does not mandate a specific rounding policy — hooks can implement any pricing function
- Hook developers must explicitly implement correct rounding in their custom curve logic
- A poorly written hook that rounds tokens_out **up** or tokens_in **down** will drain the pool over time
- Standard recommendation for custom bonding curve hooks: follow V2/V3 convention (tokens_out round down, tokens_in round up)

> [!analysis] V4 hooks transfer rounding responsibility to the hook author. This is a new attack surface: a malicious or buggy hook could implement rounding that slowly drains pool reserves, or allows traders to extract more than they paid for.

### Standard Practice Across DeFi

| Operation | Direction | Rationale |
|---|---|---|
| `tokens_out` (what trader receives) | Round **down** | Trader gets less; pool retains dust |
| `tokens_in` (what trader pays) | Round **up** | Trader pays more; pool receives extra |
| `liquidity_minted` (to LP) | Round **down** | LP gets less; pool retains dust |
| `liquidity_burned` (by LP) | Round **down** | LP withdraws less; pool retains dust |
| `fee_amount` | Round **up** | More fee collected; protects protocol |

### Bonding Curve-Specific Considerations
- Bonding curves with polynomial or exponential pricing functions (e.g., `price = a * supply^n`) require integer approximations
- Fixed-point libraries (e.g., PRBMath, ABDKMath) provide higher precision but still truncate eventually
- **Bancor's Bonding Curve**: Uses `reserveRatio` and fractional exponentiation — approximated via Taylor series with explicit round-down on output
- **Curve Finance stableswap**: Uses Newton-Raphson iteration with integer arithmetic; rounds output down, explicitly documented in code
- **Pump.fun's bonding curve**: Uses a virtual AMM with integer arithmetic; graduation threshold exact only if accumulated rounding dust is accounted for

### Pool Solvency Implications
- If `tokens_out` rounds up: pool reserves decrease faster than the invariant predicts → eventual insolvency
- If `tokens_in` rounds down: pool receives less than it should → invariant violated after enough swaps
- In a bonding curve that auto-graduates at a threshold (e.g., market cap target), rounding errors in either direction can cause the graduation trigger to fire at the wrong time or never

> [!analysis] For a bonding curve launchpad, graduation threshold logic must account for rounding dust. If graduation triggers when `collateral_raised >= THRESHOLD`, accumulated rounding losses on the input side could prevent the threshold from ever being exactly reached. A safer pattern is `collateral_raised >= THRESHOLD - DUST_TOLERANCE` with explicit dust handling at graduation.

## How it relates to Logos

- Any Logos bonding curve launchpad (RFP-015) must explicitly specify rounding direction for every arithmetic operation
- The hook-based architecture (if using V4) transfers rounding responsibility to the hook — this must be audited carefully
- Graduation threshold logic must account for rounding dust accumulation across thousands of swaps
- The [[Flaunch (Uniswap V4 Hooks Launchpad)]] PositionManager hook is a reference implementation to study for correct rounding patterns

## Open Questions
- Does PRBMath or ABDKMath64x64 provide sufficient precision for a polynomial bonding curve over the full supply range?
- What is the maximum accumulated rounding error across 1M swaps on a typical bonding curve, and does it materially affect graduation timing?
- How should dust (sub-wei-equivalent rounding residuals) be handled at graduation — burned, donated to LPs, or held in a reserve?
- Are there known exploits where rounding manipulation on a bonding curve allowed extraction of more than fair value?

## Sources
- https://github.com/Uniswap/v2-periphery/blob/master/contracts/libraries/UniswapV2Library.sol
- https://github.com/adshao/publications/blob/master/uniswap/dive-into-uniswap-v2-contracts/README.md
- https://uniswapv3book.com/milestone_4/tick-rounding.html
- https://docs.uniswap.org/contracts/v4/overview
- https://jeiwan.net/posts/programming-defi-uniswapv2-4/
