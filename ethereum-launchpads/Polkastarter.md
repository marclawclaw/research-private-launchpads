---
topic: Polkastarter
type: competitor
tags: [ethereum, polkadot, launchpad, ido, permissioned, pols-staking, lottery]
confidence: high
last_updated: 2026-04-02
sources:
  - https://polkastarter.com/
  - https://blog.polkastarter.com/how-to-participate-in-a-polkastarter-ido/
  - https://blog.polkastarter.com/all-you-need-to-know-about-pols-power/
---

## Summary
Polkastarter is a decentralised IDO launchpad (originally Polkadot-based, now multi-chain including Ethereum) that gates participation via POLS token staking. Access to IDO allowlists requires holding or staking POLS for a minimum 7 days, with allocation probability determined by a lottery system weighted by POLS Power.

## Key Facts

### Scale & Traction

> [!fact] Confirmed from Polkastarter blog (Q1 2022 recap) and CoinMarketCap
> - **Total funds raised across all IDOs:** $46M+ across 105+ projects (as of Q1 2022)
> - **Projects launched:** 110+ (as of June 2022, per CoinMarketCap)
> - **POLS token DEX liquidity TVL:** ~$3.31M (as of Dec 2024)
> - **Status:** Active but significantly reduced activity in 2024-2025 bear cycle; pivoted to gaming fund ($2M) and updated IDO processes

> [!outdated] The $46M figure is from Q1 2022 — cumulative total is likely higher but no recent aggregate data published. Polkastarter has not published updated cumulative stats since 2022.

### Mechanism
- Native token: $POLS (ERC-20 / multi-chain)
- Permissioning mechanism: POLS staking or LP token holding (Uniswap/PancakeSwap) for minimum 7 days
- Allowlist system: lottery-based — 1,000 POLS Power = eligible; +250 POLS Power = +1 extra lottery ticket per IDO
- "POLS Power" = combined weight from staked POLS + LP POLS tokens + on-chain history
- Each IDO has its own allowlist window; users apply per IDO
- KYC: handled by each individual project (not centrally by Polkastarter — unlike DAO Maker)
- Multi-chain: supports Ethereum, BNB Chain, and others
- Sale type: fixed-price IDOs with hard cap; FCFS or lottery allocation models
- Projects apply to launch; not permissionless for projects (curated)

## How it relates to Logos
- Polkastarter's POLS Power + lottery model is a Sybil-resistant access design using token stake as proof-of-commitment without full KYC
- 7-day hold requirement reduces wash trading and bots
- Per-project KYC delegation (vs DAO Maker central KYC) may map better to Logos' decentralisation values
- Lottery allocation at scale is fairer than pure first-come-first-served

> [!fact] Polkastarter requires 7-day minimum hold before IDO eligibility — creating a natural lock-in/commitment signal

> [!analysis] Lottery + stake model is more egalitarian than DAO Maker's pure tier/size model, but still token-plutocratic

## Refund & Participant Protection

> [!analysis] No native refund mechanism — IDO purchases are final once executed

- **Refund window:** No. Once a participant successfully purchases tokens in a Polkastarter IDO, the transaction is final. There is no grace period or cooling-off window for refunds.
- **Minimum raise threshold (soft cap):** No evidence of soft cap / minimum raise mechanics. IDOs have a hard cap (maximum) but no documented minimum threshold that would trigger automatic refunds if unmet.
- **Post-launch performance refund:** No. Polkastarter does not offer DYCO-style performance-based refunds. Token performance post-launch is entirely market-driven.
- **Cancellation rights:** Pre-sale only. Participants who are allowlisted but have not yet completed their purchase can choose not to participate. Once the swap transaction is executed on-chain, it is irreversible.

> [!analysis] Polkastarter's participant protection model relies on *access gating* (POLS staking + lottery) rather than post-purchase refund rights. The theory is that requiring 7-day staking commitment and lottery selection filters for committed participants, reducing the need for refund mechanisms. However, this provides no protection against post-launch token underperformance.

## Allowlist & Access Control

> [!fact] Confirmed from Polkastarter blog (tier system, allowlist updates), support docs, and POLS Power guide

- **Gating method:** Token staking ($POLS) + lottery system + per-project KYC
- **Enforcement:** Hybrid — on-chain staking/holding verification (POLS in wallet or staking contract for 7+ days), off-chain lottery selection and KYC handled per-project
- **Tiered access:** Yes — POLS Power tier system with booster multipliers:
  - Minimum: 1,000 POLS Power (raised from 250 in 2024) = eligibility for allowlist lottery
  - Every 1,000 POLS Power = 4 lottery tickets (1 ticket per 250 POLS)
  - Tier 1,000+ POLS Power: 1.1x booster (every ticket worth 1.1 tickets)
  - Tier 3,000+ POLS Power: 1.15x booster
  - Tier 10,000+ POLS Power: 1.20x booster
  - Tier 30,000+ POLS Power: 1.25x booster + No Cooldown between IDOs
  - Tier 50,000+ POLS Power: Guaranteed spots in sales (added 2024)
  - Multiple tickets increase winning chances but NOT the maximum allocation — egalitarian allocation once selected
- **POLS Power sources:** Three qualifying paths:
  1. Hold POLS in wallet for minimum 7 days
  2. Hold POLS LP tokens (Uniswap/PancakeSwap) for minimum 7 days
  3. Stake POLS on dashboard (instant eligibility but tokens locked for 7 days)
- **Geo-blocking:** Varies per project — KYC is delegated to individual projects (not centrally managed by Polkastarter). Each project can implement its own jurisdictional restrictions
- **Phased rounds:** Yes — each IDO has its own allowlist application window. Users must actively apply per IDO. Whitelist-only round → if any tokens remain, may move to FCFS
- **Sybil resistance:** Medium-strong — combination of:
  - 7-day minimum hold/stake requirement (prevents wash trading and last-minute gaming)
  - Economic cost of acquiring 1,000+ POLS
  - Per-project KYC (identity verification reduces multi-wallet attacks)
  - Cooldown period between IDO participations for lower tiers
  - Lottery system means even whales can't guarantee selection (except 50k+ tier)

> [!analysis] Polkastarter's lottery model is more egalitarian than DAO Maker's pure tier system — even small holders (1,000 POLS) can win allocation, while DAO Maker effectively locks out sub-2,000 DAO holders. However, the 50k+ guaranteed tier (added 2024) introduces a whale-friendly escape hatch. The 7-day hold requirement is an elegant Sybil-resistance mechanism that doesn't require KYC, but per-project KYC delegation means inconsistent enforcement across the platform.

See also: [[Token Sale Permissioning Mechanisms]], [[Off-Chain Whitelist Pattern (Merkle Proof)]]

## Fee Structure

> [!analysis] Fee details partially inferred — Polkastarter does not publish a comprehensive public fee schedule

- **Platform fee (issuer):** Fixed fee paid by pool creators, reported as ~1% of raised amount (deducted from proceeds). Exact percentage may vary per deal and is not prominently documented
- **Participant fee (buyer):** Transaction fees paid in $POLS. Standard network gas fees apply. No additional percentage fee charged to buyers
- **Listing/setup fee:** Not publicly disclosed. Projects must apply and be accepted (curated platform). Likely involves token allocation agreements with Polkastarter team
- **Staking requirement:** Minimum 1,000 POLS Power (raised from 250 in 2024) for lottery eligibility. At current prices (~$0.30-0.50/POLS), this is approximately $300-500 minimum. Top tier (50,000 POLS for guaranteed spots) costs ~$15,000-25,000
- **Gas/proof costs:** Standard network gas fees borne by participants. Multi-chain support (Ethereum, BNB Chain) means gas costs vary by chain
- **Revenue model:** (1) Pool creation fees from projects, (2) transaction fees paid in $POLS, (3) token allocations from launched projects, (4) fee-sharing with $POLS stakers (planned governance model), (5) $POLS token value from utility demand

> [!analysis] Polkastarter's fee model is less transparent than Fjord Foundry or DAO Maker. The ~1% pool creation fee is the lowest platform fee of the major launchpads, but the real cost is the staking requirement — projects need to attract POLS stakers, and participants need $300-25,000+ in POLS to participate. The staking cost functions as an implicit fee/barrier.

## Sale Lifecycle & Close Mechanics

> [!analysis] Polkastarter does not publish comprehensive smart contract documentation; lifecycle inferred from participation guides, blog posts, and platform behavior

- **Manual close (issuer):** No evidence of issuer-initiated early close. IDO pools are configured with fixed parameters (token amount, price, duration) and run until the hard cap is reached or time expires. The Polkastarter team manages the pool deployment — individual projects do not have direct smart contract control to end sales early.
- **Automatic close triggers:** Two primary triggers: (1) **Hard cap reached** — pool is fully subscribed, no more swaps accepted. (2) **Time expiry** — the IDO window closes at the scheduled end time. IDOs are typically short (minutes to hours), with FCFS mechanics meaning they often sell out quickly. No documented soft cap / minimum raise threshold.
- **Emergency halt/pause:** Not documented for individual IDOs. Polkastarter as the platform operator likely has the ability to pause or cancel pools, but this is not exposed to project teams or documented publicly. The smart contract swap pools are deployed by Polkastarter, suggesting the platform retains admin control.
- **Admin override:** Likely yes — Polkastarter deploys and manages the IDO smart contracts. As the contract deployer/admin, the platform likely has privileged functions to pause or cancel pools. However, this is not publicly documented.
- **Resume after pause:** Unknown — no documentation on pause/resume mechanics for IDO pools.
- **Post-close behavior:** Automatic swap execution. Polkastarter IDOs use fixed-price swap pools — participants send payment tokens and receive project tokens in a single atomic transaction. There is no separate "claim" step; the swap is immediate on-chain. Post-IDO, tokens are in participants' wallets immediately (subject to any vesting schedule configured by the project, which is separate from the IDO itself).
- **Enforcement:** On-chain (smart contract swap pools). The IDO itself is a set of smart contract interactions — swaps are executed atomically on-chain. However, the allowlist/lottery selection and KYC are off-chain, creating a hybrid model where access is off-chain but execution is on-chain.

> [!analysis] Polkastarter's IDO model is transaction-based (atomic swaps) rather than pool-based (LBP) or allocation-based (SHO). This means there's no "open sale window" to pause — each participant's transaction either succeeds or fails independently. The FCFS nature means most IDOs sell out in minutes, making pause/close mechanics less relevant operationally. The lack of documented admin controls is a transparency gap.

## Open Questions
- Is the POLS allowlist contract open source and audited?
- What's Polkastarter's current traction in 2025/2026 — is it still active?
- How does cross-chain allowlist verification work technically?

## Sources
- https://polkastarter.com/
- https://blog.polkastarter.com/how-to-participate-in-a-polkastarter-ido/
- https://blog.polkastarter.com/all-you-need-to-know-about-pols-power/
- https://support.polkastarter.com/article/22-how-staking-works
