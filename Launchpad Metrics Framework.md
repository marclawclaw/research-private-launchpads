---
topic: Launchpad Metrics Framework
type: concept
tags: [metrics, tvl, volume, revenue, launchpad, methodology]
confidence: high
last_updated: 2026-04-02
sources:
  - internal analysis
---

## Summary

Token launch platforms (launchpads) are **transactional protocols** — funds flow through them briefly during token sales, then move on. This makes them fundamentally different from DeFi lending pools or AMMs where capital is persistently locked. Using TVL (Total Value Locked) to evaluate launchpads is misleading because there is no meaningful "locked" value; deposits exist only for the duration of a sale window (often hours to days).

This note defines the correct metrics for comparing launchpad protocols and clarifies when TVL is and isn't appropriate.

## Why TVL Doesn't Apply to Launch Platforms

> [!analysis] TVL measures capital persistently committed to a protocol — liquidity in AMM pools, collateral in lending markets, assets in vesting contracts. Token launch platforms don't hold capital persistently:
> - **Pump.fun:** Bonding curve deposits exist only until graduation to DEX (~minutes to hours)
> - **[[Metaplex Genesis]]:** Launch Pool deposits exist for the configured deposit window (1hr for memecoins, ~48hr for projects), then funds are distributed
> - **[[DAOs.fun]]:** Investment DAO raises last 7 days, then funds are deployed by the manager
> - **[[ethereum-launchpads/Fjord Foundry]]:** LBP sales typically last 24-72 hours
>
> Reporting TVL for these protocols either captures a momentary snapshot of in-flight capital (meaningless for comparison) or conflates a separate product (e.g., Pumpswap DEX) with the launch platform itself.

## Correct Metrics for Comparing Launchpads

| Metric | Definition | Why it matters |
|--------|-----------|---------------|
| **Total Funds Raised (cumulative)** | Sum of all capital deposited into launches over the protocol's lifetime | Primary scale metric — analogous to GMV for marketplaces |
| **Funds Raised per period** | Capital raised in a given quarter/month | Growth trajectory and market cycle sensitivity |
| **Number of launches** | Count of token sales conducted | Adoption breadth; high count + low avg raise = memecoin-dominated |
| **Average raise size** | Total funds raised / number of launches | Market positioning: micro-launches (Pump.fun) vs structured raises (Genesis, Fjord) |
| **Protocol revenue** | Fees collected by the protocol | Business viability; directly comparable across platforms |
| **Unique participants** | Distinct wallets/users participating in launches | Demand-side adoption; watch for Sybil inflation |
| **Post-launch liquidity contribution** | Capital routed to DEX liquidity pools after launch | Ecosystem value creation beyond the sale itself |

> [!analysis] **Deriving funds raised from revenue:** When only protocol revenue is available (e.g., from DefiLlama), funds raised can be estimated by dividing revenue by the fee rate. For example, [[Metaplex Genesis]] charges 2% on deposits, so $1M in revenue implies ~$50M in funds raised. This is approximate — refunds, partial fills, and fee-exempt transactions introduce error. Always mark derived figures as estimates.

## Per-Period Metrics: Essential for Trend Analysis

> [!analysis] Cumulative totals (e.g., "Pump.fun has generated $987M in all-time revenue") are useful for scale comparison but obscure the trajectory of demand. Per-period breakdowns — monthly or quarterly — are essential for understanding:

- **Growth rates:** Month-over-month (MoM) and quarter-over-quarter (QoQ) changes reveal acceleration or deceleration. Pump.fun's 19x QoQ jump in Q2 2024 signals explosive adoption; the subsequent decline from Q1 2025 onward signals market saturation.
- **Seasonality:** Crypto launchpad activity correlates with broader market cycles. Q4 2024 and Q1 2025 were peak periods across Solana launchpads, coinciding with the memecoin mania. Monthly data reveals intra-quarter patterns (e.g., Genesis peaked in Aug–Oct 2025 then dropped off sharply in Dec).
- **Demand trajectory:** A platform with $100M cumulative revenue could be growing ($10M → $20M → $30M → $40M per quarter) or dying ($40M → $30M → $20M → $10M). Only per-period data distinguishes these.
- **Competitive timing:** Comparing per-period data across platforms reveals market share shifts — e.g., when Genesis gained share of Metaplex total revenue (18% in Oct 2025) vs when Pump.fun's dominance peaked.

When deriving per-period volume from revenue data, always note the fee rate used and mark derived figures as estimates. See individual competitor notes ([[Metaplex Genesis]], [[Pump.fun]]) for per-period tables.

## When TVL IS Appropriate

TVL remains the correct metric for protocols where capital is persistently locked:

- **Vesting/streaming protocols** ([[vesting-protocols/Streamflow Finance]], [[vesting-protocols/Sablier Protocol]], [[vesting-protocols/Hedgey Finance]]) — tokens locked in vesting contracts for months/years
- **AMM/DEX liquidity** (Pumpswap, Raydium, Uniswap) — LP capital committed to trading pools
- **Staking protocols** — capital locked for network security or governance
- **Lending protocols** — collateral deposited for borrowing

> [!analysis] Some platforms span both categories. Pump.fun's launch platform (bonding curves) should use transactional metrics, while Pumpswap DEX TVL (~$193M as of Q1 2026) is a valid TVL measurement because it represents persistent AMM liquidity. These should be reported separately and not conflated.

## How it relates to Logos

- A Logos-based launchpad should be evaluated using transactional metrics (funds raised, launches, participants) rather than TVL
- Protocol revenue is the most comparable cross-chain metric since fee structures vary but revenue is always denominated in value terms
- Privacy-preserving launches add a unique metric dimension: **shielded participation rate** (% of participants using private channels)
- [[ZK Token Issuance Patterns]] could enable verifiable aggregate metrics (total raised, participant count) without revealing individual positions

## Open Questions

- Is there a standard taxonomy for launchpad metrics used by analytics platforms (DefiLlama, Messari, Dune)?
- How should failed/cancelled launches be counted in cumulative metrics?
- For bonding curve platforms, should "funds raised" include all trading volume or only net capital that reaches graduation?

## Sources
- Internal analysis based on protocol mechanics review
