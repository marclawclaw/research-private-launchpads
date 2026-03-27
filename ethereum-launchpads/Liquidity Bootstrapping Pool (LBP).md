---
topic: Liquidity Bootstrapping Pool (LBP)
type: concept
tags: [ethereum, lbp, price-discovery, token-sale, balancer]
confidence: high
last_updated: 2026-03-27
sources:
  - https://balancer.gitbook.io/balancer/smart-contracts/smart-pools/liquidity-bootstrapping-faq
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
---

## Summary
A Liquidity Bootstrapping Pool (LBP) is a dynamic AMM-based token sale mechanism originally developed on Balancer. Pool weights shift over time (typically from token-heavy to collateral-heavy), causing price to decline unless demand keeps buying pressure up. This enables fair price discovery and discourages bots.

## Key Facts
- Originated from Balancer smart pools (v1 docs now deprecated, v2 maintained at docs.balancer.fi)
- Mechanics: two-asset pool (project token + collateral, usually USDC or WETH) with shifting weights
- Starting weights typically 99/1 (token/collateral) → ending 1/99; starting price set ~6–10× fair value
- `updateWeightsGradually` triggers the weight shift; `pokeWeights` (public function) advances it on schedule
- Price naturally falls if no buying; buying pushes price up temporarily
- Arbitrageurs are incentivized to correct mispricing — creates organic price discovery
- Anti-bot property: early sniping is discouraged because price starts high and falls
- Duration: Balancer recommends minimum 3 days (default minimum ~2 weeks in smart pool code)
- Sale creator recovers: remaining tokens + collateral raised (minus fees) by calling `removeToken` or removing liquidity
- Optional: pause swaps, delayed start, max 10% swap fee to discourage front-running at launch
- Platforms implementing LBPs: [[Fjord Foundry]], Copper (merged into Fjord), Balancer directly

## How it relates to Logos
- LBPs provide a trust-minimised price discovery mechanism requiring no pre-set valuation — useful for Logos projects at early token launch stage
- The shift from permissioned VC rounds to open LBP launches aligns with Logos' decentralisation ethos
- Weight-based pricing is a smart contract primitive that could be adapted for permissioned Logos token sales

> [!fact] LBP is a well-established mechanism with many successful launches (Autonolas raised $550k from $50k initial liquidity; others raised $3M+)

> [!analysis] LBPs are fundamentally open/permissionless by design; adding permissioning (whitelist) is a layer on top, not native to the mechanism

## Open Questions
- Can LBPs be combined with ZK-proof identity gating (e.g., prove KYC without revealing address)?
- How does Fjord's "zero liquidity LBP" work at the smart contract level vs. classic Balancer LBP?

## Sources
- https://balancer.gitbook.io/balancer/smart-contracts/smart-pools/liquidity-bootstrapping-faq
- https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
