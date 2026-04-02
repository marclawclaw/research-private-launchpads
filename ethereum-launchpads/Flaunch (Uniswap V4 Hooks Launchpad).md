---
topic: Flaunch (Uniswap V4 Hooks Launchpad)
type: competitor
tags: [ethereum, uniswap-v4, hooks, bonding-curve, memecoin, launchpad, base, fee-sharing]
confidence: high
last_updated: 2026-04-02
sources:
  - https://github.com/flayerlabs/flaunchgg-contracts
  - https://www.bankless.com/read/how-to-launch-better-memecoins-on-flaunch
  - https://blockworks.co/news/uniswap-v4-goes-live
  - https://docs.flaunch.gg/flaunch-docs/core-features/devs-get-revs
---

## Summary
Flaunch is a memecoin launchpad on Base built by Flayer Labs that uses Uniswap V4 hooks to implement a bonding curve and fair launch mechanism entirely within a single Uniswap V4 pool. Unlike traditional launchpads (e.g., pump.fun) that deploy a separate bonding curve contract and migrate liquidity to a DEX, Flaunch keeps the token in a single V4 pool from inception, with hooks governing pricing and fee routing at every stage. After launch, 100% of trading fees can be routed back to creators and automated buybacks in perpetuity.

## Key Facts

> [!fact] Flaunch launched on Base in late January 2025 and was the first production launchpad to leverage Uniswap V4 hooks at scale. It returned over $628,900 in revenue to creators within the first 2 days.

> [!outdated] No cumulative volume, TVL, or total tokens launched data found as of April 2026. Flaunch is tracked on DefiLlama (defillama.com/protocol/flaunch) but the page was not accessible during crawl. The $628.9K figure is the only confirmed traction metric, from the first 48 hours post-launch. The platform is relatively new (Jan 2025) and may not yet have published aggregate statistics.

### Architecture: Hooks as Bonding Curve
- The bonding curve logic lives inside a **Uniswap V4 hook contract** (specifically the `PositionManager` and `FairLaunch` contracts), not in a separate launchpad contract
- All token pricing, supply release, and fee routing are executed via hook callbacks (`beforeSwap`, `afterSwap`, etc.) on the V4 PoolManager
- The token **never leaves a single venue**: it starts in a V4 pool under hook-governed pricing and graduates to standard AMM behaviour in the same pool
- The hook overrides spot price during the fair launch phase, enforcing a fixed price regardless of pool reserves

### Phase 1: Fixed-Price Fair Launch (30 minutes)
- During the fair launch window, all buyers pay the **same fixed price** — no first-mover advantage, no instant price spikes
- Buyers **cannot sell** during this phase; all proceeds go to a Progressive Bid Wall (see below)
- If allocated supply sells out before 30 minutes, the phase ends early
- After the fair launch, early buyers are guaranteed to exit at their entry price (minus AMM swap fee) — the bid wall provides this floor

> [!fact] The fair launch phase solves the classic pump.fun problem: no sniping, no insider pre-buy, guaranteed exit at entry price.

### Phase 2: AMM Graduation (Atomic)
- After 30 minutes (or sell-out), the hook switches the pool to standard V4 constant-product pricing
- Graduation is **atomic and trustless**: the hook itself triggers the transition, no admin action required
- Remaining token supply is now traded at market price via the standard AMM curve
- There is no separate migration transaction or liquidity movement — the pool stays the same

### Fee Routing via Hooks
- V4 hooks intercept all swap fees before they reach LPs
- Creators set a **fee split at launch (0–100%)** between:
  1. **Creator revenue** — paid in ETH (converted via Internal Swap Pool to avoid token dumps)
  2. **Auto-buyback** — funds Progressive Bid Walls (see below)
  3. **Treasury** — optional accumulation for community governance
- **FLAY token holders** can turn on a protocol fee switch to collect 10% of all Flaunch protocol fees
- Dev fees are always converted to `flETH` (Flaunch's ETH-equivalent token) via an internal swap pool, so no negative token selling pressure

### Progressive Bid Wall (PBW)
- Every 0.1 ETH in trading fees automatically funds a Progressive Bid Wall
- The PBW is itself a **Uniswap V4 hook** that places a limit buy order just below the current spot price
- As price rises, the bid wall follows — stacking deeper buy-side liquidity
- This creates a **perpetual price floor** that scales with trading volume

### Revenue Model vs. pump.fun
| Feature | pump.fun | Flaunch |
|---|---|---|
| Creator fee | 0% | 0–100% (configurable) |
| Fee mechanism | Platform extracts | Hooks route to creator |
| Price floor | None | Progressive Bid Wall |
| Graduation | Separate Raydium migration | Atomic hook switch |
| Token venue | Bonding curve → DEX (two venues) | Single V4 pool forever |

### Contract Addresses (Base Mainnet)
- `PositionManager`: `0x51Bba15255406Cfe7099a42183302640ba7dAFDC`
- `FairLaunch`: `0xCc7A4A00072ccbeEEbd999edc812C0ce498Fb63B`
- `BidWall`: `0x66681f10BA90496241A25e33380004f30Dfd8aa8`
- `Flaunch` (main): `0x6A53F8b799bE11a2A3264eF0bfF183dCB12d9571`

### Import Feature
- External tokens (from Zora, Virtuals, etc.) can be imported into Flaunch to benefit from V4 hooks fee routing
- This enables retrospective creator revenue for already-launched tokens

## How it relates to Logos

> [!analysis] Flaunch's core innovation — putting bonding curve logic in a hook rather than a separate contract — is directly relevant to Logos RFP-015 (bonding curve launchpad). The architecture demonstrates that a single V4 pool can handle the full token lifecycle without liquidity migration risk.

Key relevance points:
1. **Bonding curve via hooks is production-validated** — not theoretical. Flaunch proves it works on a live mainnet with real volume.
2. **Atomic graduation** — the bonding-curve-to-AMM transition without migration solves the trust gap identified in RFP-015 comments. No rug between phases.
3. **Fee routing perpetually** — the revenue-share model (creator earns from every trade forever) is a novel incentive alignment mechanism that Logos could adopt.
4. **Privacy limitation** — Flaunch is fully transparent (Base/Ethereum). A Logos version would need to layer ZK privacy on top (e.g., private participation during fair launch phase).
5. **Progressive Bid Wall** — this auto-buyback mechanism using hooks is novel and could be adapted for Logos tokens to provide price stability without centralised market-making.

> [!analysis] The Flaunch approach is the best current reference implementation for the "hook-based bonding curve" architecture. Any Logos bonding curve launchpad should study the PositionManager and FairLaunch contracts as primary references.

## Open Questions
- Can the fixed-price fair launch phase be made private (ZK-hidden bids) while still using V4 hooks?
- What are the gas costs of the hook overhead vs. a standalone bonding curve contract?
- Does the Progressive Bid Wall hook create any MEV extraction opportunities during bid wall placement?
- Is there a minimum raise threshold / soft cap in the FairLaunch contract, or does it always graduate?
- Can the fee split be changed post-launch, or is it set immutably at creation?

## Sources
- https://github.com/flayerlabs/flaunchgg-contracts (official contracts, README)
- https://www.bankless.com/read/how-to-launch-better-memecoins-on-flaunch
- https://blockworks.co/news/uniswap-v4-goes-live
- https://docs.flaunch.gg/flaunch-docs/core-features/devs-get-revs
- https://www.npmjs.com/package/@flaunch/sdk
