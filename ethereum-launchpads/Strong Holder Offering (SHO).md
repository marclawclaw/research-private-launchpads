---
topic: Strong Holder Offering (SHO)
type: concept
tags: [ethereum, dao-maker, token-sale, permissioned, tier-system]
confidence: high
last_updated: 2026-03-27
sources:
  - https://medium.com/@yanytsky19/dao-maker-v2-strong-holding-offering-101-1a5ff862f7ff
  - https://coinmarketcap.com/alexandria/article/what-is-dao-maker
---

## Summary
Strong Holder Offering (SHO) is DAO Maker's proprietary permissioned token sale model where access is gated by staking $DAO tokens. The more $DAO staked, the higher the tier and the larger the guaranteed allocation. KYC is platform-managed and required for all participants.

## Key Facts
- Developed by [[DAO Maker]]
- Participation requires: (1) KYC on DAO Maker platform, (2) staking $DAO tokens
- Allocation = proportional to staked $DAO amount → tier assignment via on-chain analysis
- Previously: minimum 2,000 $DAO to qualify; v2 adjusted thresholds
- Three rounds typical: early/priority round for high-tier holders, then public/FCFS round
- DAO Power (derived from staked $DAO) is "allocated" to specific sales — acts like a voucher system
- Projects benefit from built-in community of vetted, staked holders (signal of quality audience)
- SHO complements SEED sales (institutional round) and DYCOs (refundable model)

## How it relates to Logos
- SHO model = economic stake as access credential — aligns token holder incentives with project success
- The "DAO Power allocation" pattern (stake once, allocate to multiple sales) is a flexible UX worth studying for a Logos ecosystem launchpad
- Can be adapted: replace $DAO stake with Logos-native token or reputation score

> [!fact] SHO creates guaranteed allocations for stakers — reduces lottery uncertainty vs. Polkastarter model

> [!analysis] Centralised KYC requirement is the main privacy concern; not compatible with Logos' privacy-first ethos without ZK uplift

## Open Questions
- Can SHO contracts be forked or licensed for use in other ecosystems?
- What's the current minimum $DAO stake threshold (as of 2026)?

## Sources
- https://medium.com/@yanytsky19/dao-maker-v2-strong-holding-offering-101-1a5ff862f7ff
- https://coinmarketcap.com/alexandria/article/what-is-dao-maker
