---
topic: Fjord Foundry
type: competitor
tags: [ethereum, launchpad, lbp, token-sale, permissioned]
confidence: high
last_updated: 2026-03-27
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

## Open Questions
- Does Fjord support on-chain KYC/identity proofs for whitelists, or only address-based allowlists?
- What chains beyond Ethereum are live?
- Is whitelist enforced via Merkle proof on-chain or off-chain API?

## Sources
- https://www.fjordfoundry.com/
- https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
- https://medium.com/@fjordfoundry/fjords-upcoming-fjo-token-lbp-and-tge-everything-you-need-to-know-32402218e77e
