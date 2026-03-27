---
topic: Token Vesting & Distribution Protocols
type: competitor
tags: [streaming, payroll, EVM, multi-chain, payments, gas-efficient]
confidence: high
last_updated: 2026-03-27
sources: [https://llamapay.io/]
---

## Summary
LlamaPay is a multi-chain EVM token streaming protocol focused on salary/payroll automation. It streams payments by the second, allowing recipients to withdraw at any time. Key differentiator is extreme gas efficiency (3.2–3.7x cheaper than alternatives) and same contract address across all EVM chains.

## Key Facts
- **Focus:** Payroll and recurring payment streaming (not primarily vesting)
- **Chains:** All EVM chains — same contract address across chains
- **Gas efficiency:** 3.2–3.7x cheaper than alternatives (e.g., Sablier)
- **Stream types:** Fixed end date or indefinite (no end date)
- **Decimals:** 20 decimal internal precision (no rounding errors)
- **Notable users:** Curve, aixbt
- **Anyone can trigger a claim:** Third-party wallets can trigger withdrawals — useful for payments to CEX addresses
- **Borrow to fund streams:** Can borrow against streams to avoid running out of balance
- **No token:** No protocol token (as of last check)

## Architecture Notes
- Single shared contract per chain — all payers use the same contract, reducing deployment costs
- Per-second streaming math: `amountPerSecond = totalAmount / durationInSeconds`
- Recipients always have access to accrued funds; no waiting for unlock periods

> [!analysis] Analyst inference — not verified
> LlamaPay prioritizes gas efficiency and simplicity over feature richness. It's the right tool for payroll; less suitable for complex investor vesting with cliffs and milestones.

> [!fact] Confirmed from official docs
> LlamaPay is used by Curve Finance and other DeFi projects for contributor payments.

## Comparison to Sablier
- **Cheaper:** 3–4x lower gas cost
- **Simpler:** Less flexible schedule customization
- **Shared contract:** No per-stream deployment cost
- **No NFT ownership:** Streams not transferable
- **No vesting-specific features:** No cliff, no milestone-based unlocks

## How it relates to Logos
- LlamaPay's gas efficiency model is a design lesson: shared contracts > per-stream deployments
- "Same address across chains" deployment pattern is useful for Logos cross-chain consistency
- The "anyone can trigger claim" feature is interesting for automated payment scenarios without requiring recipient action

## Open Questions
- Does LlamaPay support ERC-20 tokens beyond stablecoins?
- Is there a vesting/cliff feature in any version?
- What's the TVL and how active is development post-2023?
- Does LlamaPay v2 add more vesting-like features?

## Sources
- https://llamapay.io/
- https://github.com/LlamaPay/llamapay
