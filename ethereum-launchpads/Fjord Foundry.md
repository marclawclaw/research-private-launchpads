---
topic: Fjord Foundry
type: competitor
tags: [ethereum, launchpad, lbp, token-sale, permissioned]
confidence: high
last_updated: 2026-04-02
sources:
  - https://www.fjordfoundry.com/
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
---

## Summary
Fjord Foundry is an Ethereum-based token sale platform specialising in Liquidity Bootstrapping Pools (LBPs). It supports both permissionless community sales (upvote-gated) and curated/partnered sales backed by Fjord or trusted launch partners. Optional whitelisting feature restricts participation to a curated participant list.

## Key Facts
- Primary mechanism: LBPs (dynamic pricing, price starts high and decreases over time based on weight shifts)
- Two sale tiers: permissionless (community upvote) vs. curated/partnered (Fjord or launch partner backed)
- Optional whitelist: project creators can enable participant whitelisting for exclusivity
- Fee: 5% of collateral raised
- Supports zero-liquidity LBPs (synthetic/virtual collateral to generate price curve; no upfront deposit required)
- Supports buy-only or buy+sell LBP modes
- Hard cap configurable; no per-wallet limits for LBPs
- Sale duration: typically 2–5 days (3 days recommended)
- Recommended weight structure: 99/1 → 1/99 (100% token distribution target); starting price ~6–8× fair value to deter bots
- $FJO native token — NOT used to gate sales (explicit ethos: open access, no token-gating)
- Own LBP raised $15M+ in April 2024; $FJO down 70% from peak as of late 2025
- Chains: Ethereum (and others — multi-chain)
- Previously merged with Copper.co (rebranded)

## How it relates to Logos
- LBP mechanism is a model for fair, permissionless token distribution — relevant to Logos ecosystem projects needing price discovery without pre-set valuations
- Optional whitelisting feature = permissioned layer on top of open infrastructure; useful reference for hybrid open/gated designs
- Zero-liquidity LBPs lower barrier to entry for early-stage projects

> [!analysis] Fjord explicitly rejects token-gating on their own platform, distinguishing themselves from Polkastarter/DAO Maker tier models. Permissioning is optional, project-side.

## Refund & Participant Protection

> [!analysis] No native refund mechanism — LBP purchases are market trades, not subscriptions

- **Refund window:** No. LBP purchases are AMM swaps — once executed, they are final. There is no post-purchase refund window or grace period.
- **Minimum raise threshold (soft cap):** No. LBPs have no minimum raise requirement. The sale runs regardless of how much capital is deposited. If demand is low, the price simply falls to meet it.
- **Post-launch performance refund:** No. LBP tokens are freely traded on the AMM during the sale. Participants can sell back during the sale window if it's configured as buy+sell mode, but this is a market transaction at current AMM price, not a guaranteed refund.
- **Cancellation rights:** Limited. During the LBP, participants can sell tokens back into the pool (if buy+sell mode is enabled), but at market price — not at their purchase price. After the LBP ends, tokens are distributed and there is no platform-level refund mechanism.

> [!analysis] The LBP's declining-price mechanism provides *implicit* buyer protection: since price starts high and falls over time, patient buyers get better prices. Early buyers who overpay can sell back during the sale at market price, but this is not a guaranteed refund. Fjord's vesting feature (optional cliff + linear vesting post-LBP) locks tokens, further removing any post-sale refund possibility.

## Allowlist & Access Control

> [!fact] Confirmed from Fjord Foundry docs (tiered sale guide, LBP FAQ) and Bitbond review

- **Gating method:** Optional project-managed whitelist (address-based CSV upload) OR fully open (no gating). Fjord explicitly rejects platform-level token-gating — $FJO is NOT required to participate
- **Enforcement:** Off-chain (platform-level). Project creators upload a CSV of whitelisted wallet addresses during sale setup. Enforcement appears to be at the Fjord platform/UI layer, not via on-chain Merkle proofs. No evidence of on-chain whitelist contracts
- **Tiered access:** Yes — Fjord supports tiered fixed-price sales with per-tier configuration:
  - Each tier can have different token amounts for sale and price per token
  - Minimum and maximum allocation per user configurable per tier
  - Tiers are project-defined, not platform-wide (unlike DAO Maker's universal tier system)
  - LBPs themselves have no per-wallet limits or tiered access
- **Geo-blocking:** Yes — project creators can specify "Geo-blocked Countries" during sale setup to restrict participation by region. Enforcement is at the platform level
- **Phased rounds:** Yes — tiered sales support Seed, Private, and Public round types. LBPs are typically single-phase but the declining-price curve creates an implicit time-gated advantage for patient buyers
- **Sybil resistance:** Weak for LBPs (open access, no identity verification). For whitelisted tiered sales, Sybil resistance depends on how the project curates the whitelist (Fjord provides the tool, not the curation). Anti-Snipe feature can be enabled to prevent bot participation. No mandatory KYC at the platform level

> [!analysis] Fjord's permissioning philosophy is fundamentally different from DAO Maker/Polkastarter: access control is a project-side option, not a platform-enforced requirement. This makes Fjord maximally flexible but means Sybil resistance is only as strong as each project's whitelist curation process. The LBP mechanism's anti-bot properties (high starting price, declining curve) provide structural protection but not identity-level Sybil resistance.

See also: [[Token Sale Permissioning Mechanisms]], [[Liquidity Bootstrapping Pool (LBP)]]

## Open Questions
- Does Fjord support on-chain KYC/identity proofs for whitelists, or only address-based allowlists?
- What chains beyond Ethereum are live?
- Is whitelist enforced via Merkle proof on-chain or off-chain API?

## Sources
- https://www.fjordfoundry.com/
- https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
- https://medium.com/@fjordfoundry/fjords-upcoming-fjo-token-lbp-and-tge-everything-you-need-to-know-32402218e77e
