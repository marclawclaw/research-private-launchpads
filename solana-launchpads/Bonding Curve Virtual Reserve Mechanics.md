---
topic: Bonding Curve Virtual Reserve Mechanics
type: concept
tags: [bonding-curve, virtual-reserves, pump-fun, meteora, AMM, constant-product, solana]
confidence: high
last_updated: 2026-04-02
sources:
  - https://gist.github.com/rubpy/6c57e9d12acd4b6ed84e9f205372631d
  - https://docs.rs/pumpfun/latest/pumpfun/accounts/struct.BondingCurveAccount.html
  - https://docs.meteora.ag/overview/products/dbc/what-is-dbc
  - https://github.com/MeteoraAg/dynamic-bonding-curve
  - https://solana.stackexchange.com/questions/20049/how-to-compute-bonding-curve-of-pumpfun-token-based-on-specific-swap
---

# Bonding Curve Virtual Reserve Mechanics

## Summary
Both pump.fun and Meteora DBC use a dual-reserve accounting system: **virtual reserves** are synthetic pricing parameters used in the constant-product formula, completely separate from **real reserves** (actual tokens held in program vaults). The virtual reserves are always larger than real balances, allowing price discovery to start at a target initial price even before any real collateral exists.

## Key Facts

### The Core Distinction

| Reserve Type | Purpose | Real tokens? |
|---|---|---|
| **Virtual token reserve (Vt)** | Synthetic pricing parameter in `x * y = k` | ❌ No — a configured constant (initially) |
| **Virtual collateral reserve (Vc)** | Synthetic starting collateral value | ❌ No — no real collateral at start |
| **Real token reserve** | Actual SPL tokens held by program vault | ✅ Yes |
| **Real collateral reserve** | Actual SOL/quote tokens received from buyers | ✅ Yes |

### Price Formula

```
Price = Vc / Vt  (uses virtual values, not real balances)
```

The constant product invariant is maintained using the **virtual** values:
```
virtual_sol_reserves * virtual_token_reserves = k  (constant)
```

### pump.fun: Concrete Numbers (from on-chain data)

```
BondingCurveAccount {
  virtual_sol_reserves:   70,750,300,176   # larger than real
  virtual_token_reserves: 454,980,409,814,361
  real_sol_reserves:      40,750,300,176   # actual SOL received
  real_token_reserves:    175,080,409,814,361  # actual tokens remaining
  token_total_supply:     <total minted>
  complete: false
}
```

Key: `virtual_sol_reserves > real_sol_reserves` always. The difference is a fixed initial offset (~30 SOL equivalent in this example) that creates the starting price without any real collateral being deposited.

### pump.fun: Initial Configuration

- Initial virtual SOL reserve: ~30 SOL (synthetic starting collateral, zero real SOL)
- Initial virtual token reserve: ~1,073,000,000,000,000 (all tokens "virtually" available)
- Creator deposits **real** tokens (supply for sale + reserve for DEX)
- Buyers pay real SOL → accumulates as real_sol_reserves
- Tokens sold reduce both real and virtual token reserves in sync
- Graduation: when ~85% of tokens sold / ~85 SOL raised → liquidity migrates to Raydium

### Meteora DBC: Virtual Pool Design

- Uses a **virtual pool** (`VirtualPool` account) — no real AMM exists during bonding phase
- Price determined by position on the bonding curve (up to 16 configurable segments)
- `base_vault` and `quote_vault` hold **real** tokens
- Supports both **dynamic supply** (mint on buy) and **fixed supply** (pre-mint, return leftovers)
- Formula: `x * y = virtual_base_reserve * virtual_curve_reserve`
- Graduation: when `real_quote_reserve >= migration_quote_threshold` → auto-migrates to DAMM v1/v2

### What "Virtual Reserve" Does NOT Mean

> [!fact] Critical distinction — often misunderstood in RFPs and documentation
> "Virtual token reserve Vt" is NOT the total project token supply deposited by the creator. It is a **synthetic pricing parameter** set to a value *larger* than any real deposit, designed to establish an initial price `p₀ = Vc / Vt`.

The real deposit consists of:
- **D**: tokens offered for sale during bonding phase
- **R**: tokens reserved for post-graduation DEX liquidity

The virtual reserves are:
- **Vt**: set independently (Vt > D + R), determines starting price
- **Vc**: synthetic starting collateral (no real backing at genesis)

### Implications for RFP Design

1. **Pricing at genesis**: The initial price is set by choosing Vc and Vt independently of real token count. This allows a specific market cap target at launch.
2. **Constant product shifts**: As buyers purchase, both virtual and real reserves update together, but virtual values always retain the synthetic offset.
3. **Refunds and minimum raise**: If buyers can sell back (two-way curve), they redeem against real collateral. The virtual offset does not protect real collateral from depletion.
4. **Incompatibility with minimum raise**: Two-way curves allow buyers to drain real collateral, potentially undermining minimum raise thresholds.

## How it relates to Logos

- Any Logos bonding curve RFP must clearly distinguish virtual vs real reserves to avoid implementation errors
- The pump.fun model is the dominant Solana reference — implementers will look at its on-chain state and misread virtual values as real deposits if not explicitly corrected
- [[Bonding Curve Mechanics]] in RFP-015 should specify: Vt is a synthetic pricing parameter, not the real token deposit
- See also: [[Solana Launchpad Ecosystem Overview]], [[Meteora DBC]]

## Open Questions

- What is the exact formula pump.fun uses to set initial Vc/Vt for a given starting market cap?
- Does Meteora DBC expose virtual reserve values in its on-chain state like pump.fun?
- How do alternative curves (linear, sigmoid) handle the virtual reserve equivalent?

## Sources

- https://gist.github.com/rubpy/6c57e9d12acd4b6ed84e9f205372631d — on-chain BondingCurveAccount state
- https://docs.rs/pumpfun/latest/pumpfun/accounts/struct.BondingCurveAccount.html — Rust struct definition
- https://docs.meteora.ag/overview/products/dbc/what-is-dbc — Meteora DBC overview
- https://github.com/MeteoraAg/dynamic-bonding-curve — Meteora DBC source
- https://solana.stackexchange.com/questions/20049/how-to-compute-bonding-curve-of-pumpfun-token-based-on-specific-swap — Stack Exchange breakdown
