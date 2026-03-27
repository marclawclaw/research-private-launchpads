---
topic: Polkastarter
type: competitor
tags: [ethereum, polkadot, launchpad, ido, permissioned, pols-staking, lottery]
confidence: high
last_updated: 2026-03-27
sources:
  - https://polkastarter.com/
  - https://blog.polkastarter.com/how-to-participate-in-a-polkastarter-ido/
  - https://blog.polkastarter.com/all-you-need-to-know-about-pols-power/
---

## Summary
Polkastarter is a decentralised IDO launchpad (originally Polkadot-based, now multi-chain including Ethereum) that gates participation via POLS token staking. Access to IDO allowlists requires holding or staking POLS for a minimum 7 days, with allocation probability determined by a lottery system weighted by POLS Power.

## Key Facts
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

## Open Questions
- Is the POLS allowlist contract open source and audited?
- What's Polkastarter's current traction in 2025/2026 — is it still active?
- How does cross-chain allowlist verification work technically?

## Sources
- https://polkastarter.com/
- https://blog.polkastarter.com/how-to-participate-in-a-polkastarter-ido/
- https://blog.polkastarter.com/all-you-need-to-know-about-pols-power/
- https://support.polkastarter.com/article/22-how-staking-works
