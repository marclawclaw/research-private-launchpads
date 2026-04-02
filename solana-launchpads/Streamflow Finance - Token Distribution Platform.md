---
topic: Solana Token Launchpads & Permissioned Sales
type: competitor
tags: [solana, vesting, distribution, streamflow, airdrop, staking]
confidence: high
last_updated: 2026-04-02
sources:
  - https://streamflow.finance/
  - https://streamflow.finance/blog/token-vesting-the-definitive-guide
---

# Streamflow Finance — Token Distribution Platform

## Summary
Streamflow is the dominant Solana token distribution platform with $1.4B+ TVL, 28.5K+ projects, and 1.3M+ users. It provides automated vesting schedules, airdrops, staking-as-a-service, and on-chain payroll. It also offers a white-label portal product for custom-branded distribution UX. Listed on official Solana docs under "token vesting."

## Key Facts
- **TVL:** $1.4B+
- **Projects using it:** 28,500+
- **Users:** 1.3M+
- **Core products:**
  - **Vesting contracts:** Linear, cliff, milestone-based schedules; batch setup; automatic wallet delivery
  - **Airdrops:** Batch payout tooling, minimizes manual errors
  - **Staking-as-a-service:** Set up staking in clicks, customizable rewards, real-time stake data
  - **Token locks:** Lock dashboards
  - **On-chain payroll / subscriptions:** Streaming payments use case
- **SDK available** for dApp integration — programmable token transfer features
- **White-label portals:** Custom-branded airdrop/claim portals, staking pages, lock dashboards for projects
- **Multi-chain:** Primarily Solana, also EVM (noted in discovery research)
- Notable customers: Heavenland, BONK, UXD
- Listed in official Solana documentation
- **USD+:** New product (stablecoin-adjacent) launched ~2026

> [!fact] $1.4B TVL and 28.5K projects from official Streamflow homepage (March 2026)

> [!analysis] Streamflow is infrastructure, not a launchpad itself — it handles post-sale distribution, not the sale/price-discovery phase. A complete launchpad would use Streamflow for vesting after a separate sale mechanism.

## How it relates to Logos
- Streamflow's SDK could be the vesting/distribution layer for a Logos token sale — integrate for post-sale token release schedules
- White-label portals demonstrate the pattern of "bring your own brand" distribution infra — a Logos-native equivalent could layer privacy (Waku notifications, Codex storage) on top
- Streamflow's composable model (vesting + airdrop + staking as separate primitives) aligns with Logos' modular stack philosophy

## Refund & Participant Protection

> [!fact] Cancellation mechanics confirmed from Streamflow documentation

- **Refund window:** Not applicable — Streamflow is post-sale distribution infrastructure, not a sale platform.
- **Minimum raise threshold (soft cap):** Not applicable.
- **Post-launch performance refund:** Not applicable.
- **Cancellation rights:** Yes — configurable at contract creation. On cancellation: vested tokens go to recipient, unvested tokens return to sender. This is an issuer/sender-initiated clawback, not an investor refund right.

> [!analysis] Streamflow provides issuer-side revocability (cancellation of vesting), which is useful for team member departures or compliance clawbacks. It does not provide participant-initiated refund capabilities. A launchpad using Streamflow for post-sale vesting would need to layer refund logic separately.

## Open Questions
- Does Streamflow support permissioned claims (i.e., KYC-gated airdrops or vesting that requires credential verification)?
- What's the smart contract audit status?
- Does the SDK expose vesting state for on-chain composability (e.g., governance voting based on unvested allocations)?
- Is there support for privacy-preserving distribution (hidden allocations)?

## Sources
- https://streamflow.finance/
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
