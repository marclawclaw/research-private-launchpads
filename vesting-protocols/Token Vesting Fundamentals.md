---
topic: Token Vesting & Distribution Protocols
type: concept
tags: [vesting, tokenomics, distribution, smart-contracts]
confidence: high
last_updated: 2026-03-27
sources: [https://streamflow.finance/blog/token-vesting-the-definitive-guide]
---

## Summary
Token vesting locks tokens and releases them gradually over a predefined schedule, preventing immediate sell-offs and aligning stakeholder incentives with long-term project success. It's the crypto equivalent of equity vesting in traditional finance — a critical mechanism for sustainable tokenomics.

## Key Facts
- **Purpose:** Control token supply introduction, prevent market dumps, reward long-term commitment
- **Common recipients:** Core team, VCs/investors, DAO treasury, ecosystem incentives, public sale participants
- **Typical duration:** 1–4 years with optional cliff periods
- **Two modes:** Off-chain (manual, centralized, opaque) vs. on-chain (automated, auditable, trustless)
- **Cliff:** A period during which no tokens unlock; after cliff a portion releases, then linear vesting begins
- **Standard design:** "1-year cliff + 4-year linear" is the industry norm for team/investor allocations

## Types of Vesting Schedules
| Type | Description | Use Case |
|------|-------------|----------|
| Linear | Tokens unlock evenly over time | Team, investors |
| Cliff | No release until cliff date, then linear | Investor confidence |
| Milestone-based | Release tied to project deliverables | Grants, bounties |
| Twisted/Randomized | Unpredictable intervals | Gamified/community ecosystems |

## On-Chain vs Off-Chain
- **Off-chain:** Tokens held by founders or CEX wallets, manual releases, not publicly auditable, error-prone
- **On-chain:** Smart contracts enforce schedule automatically, fully auditable, reduces admin burden, higher trust

## How it relates to Logos
- Any token-based incentive program on Logos (team allocations, ecosystem grants, community airdrops) needs a vesting mechanism
- On-chain vesting protocols could be integrated into launchpad infrastructure built on Logos
- Privacy-preserving vesting (hiding allocations until unlock) is a potential differentiator for privacy-focused chains

## Open Questions
- Can vesting schedules incorporate ZK proofs to hide allocation amounts while still enforcing rules on-chain?
- What's the gas/fee overhead of on-chain vesting on different chains vs Logos' architecture?
- How do milestone-based vesting contracts verify off-chain conditions (oracle dependency)?

## Sources
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
