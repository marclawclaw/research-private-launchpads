---
topic: Solana Token Launchpads & Permissioned Sales
type: concept
tags: [vesting, tokenomics, distribution, cliff, linear, milestone]
confidence: high
last_updated: 2026-03-27
sources:
  - https://streamflow.finance/blog/token-vesting-the-definitive-guide
---

# Token Vesting Schedules

## Summary
Token vesting locks an allocation and releases it incrementally over time according to a predefined schedule. It prevents token dumps, aligns stakeholder incentives with long-term project success, and builds investor confidence. On-chain vesting via smart contracts is the gold standard — fully auditable and automated.

## Key Facts

### Vesting types
| Type | Description | Common use |
|------|-------------|------------|
| **Linear** | Tokens unlock evenly per period (e.g., 25%/year over 4 years) | Team, investors |
| **Cliff** | No tokens until cliff date, then a portion unlocks + linear continues | Team (e.g., 1-year cliff, then monthly) |
| **Milestone-based** | Tokens unlock on product/metric achievements | DAO grants, KPI incentives |
| **Twisted/randomized** | Unpredictable release intervals | Gamified/experimental ecosystems |

### Stakeholder groups typically vested
- Core team & advisors (reduce early exits)
- VCs & private investors (reduce immediate sell pressure)
- DAO treasury (fund governance/ops over time)
- Ecosystem incentives / community programs
- Public sale participants (prevent post-IDO dumps)

### On-chain vs off-chain vesting
- **Off-chain:** Tokens held by founders or CEX — manual release, opaque, rug-pull risk
- **On-chain:** Smart contract enforces schedule — fully auditable, automated, no single point of control

### Security properties
- Smart contract enforcement eliminates human error in releases
- Blockchain transparency allows community/investors to verify allocations
- Prevents rug pulls and insider dumping when properly designed

> [!fact] Confirmed from Streamflow's definitive guide (Nov 2022, still referenced in 2026 docs)

> [!analysis] The biggest vesting risk is schedule design (insiders can still dump at cliff), not the technical implementation. Milestone-based vesting is theoretically better aligned but harder to enforce trustlessly on-chain.

## How it relates to Logos
- Any Logos token sale would need a vesting layer for team/investor allocations — Streamflow SDK is the ready-made choice
- Milestone-based vesting with on-chain verification could integrate with Logos governance (Nomos) for trustless milestone confirmation
- Privacy-preserving vesting (hidden allocation amounts) is an open research gap — aligns with Logos' confidentiality goals

## Open Questions
- Can vesting schedules be made private (amounts hidden, only recipient knows their allocation)?
- How do vesting contracts interact with governance — can unvested tokens still vote?
- What happens to unvested tokens if a team member leaves?

## Sources
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
