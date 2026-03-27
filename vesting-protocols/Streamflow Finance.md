---
topic: Token Vesting & Distribution Protocols
type: competitor
tags: [vesting, streaming, Solana, distribution, airdrops, payroll]
confidence: high
last_updated: 2026-03-27
sources: [https://streamflow.finance/vesting, https://streamflow.finance/blog/token-vesting-the-definitive-guide]
---

## Summary
Streamflow is a Solana-native token distribution platform offering vesting, airdrops, staking, and on-chain payroll. It focuses on low-fee, high-speed token stream management with batch CSV upload and SDK integration. Primary chain is Solana, positioning it as the Sablier equivalent for the Solana ecosystem.

## Key Facts
- **Primary chain:** Solana (low fees, fast finality)
- **Features:** Token vesting, airdrops, staking, token locks, token mint, token dashboard, payroll
- **Vesting features:** Auto-claim, cliff support, initial allocation, batch transfers via CSV, automated notifications
- **Security audits:** FYEO and OPCODES on Solana
- **SDK:** Programmable API for dApp integration and novel use cases
- **Batch vesting:** Set up contracts for all recipients at once, automatic transfers on unlock
- **Token:** STREAM (stakeable via Streamflow Foundation)
- **Target users:** Projects doing IDOs, DAOs, gaming platforms, DeFi protocols

## Differentiators vs Sablier
| Feature | Streamflow | Sablier |
|---------|-----------|---------|
| Primary chain | Solana | EVM (27 chains) + Solana |
| Solana-native | Yes | Secondary (newer) |
| Fees | Low (Solana fees) | EVM gas |
| SDK | Yes | Yes |
| Airdrops | Yes | Yes (Merkle-based) |
| Staking | Yes | No |
| Token | STREAM | None (protocol-owned) |

> [!analysis] Analyst inference — not verified
> Streamflow's Solana focus gives it a speed/cost advantage but limits it to the Solana ecosystem. For multi-chain launchpads, Sablier is more flexible.

## How it relates to Logos
- If Logos runs on or bridges to Solana, Streamflow is a direct integration candidate
- The SDK-first approach is a good pattern: launchpad builders can embed vesting without building it themselves
- Streamflow's "token dashboard" product (track all distributed tokens) is a useful reference for investor/team UX

## Open Questions
- Does Streamflow support EVM chains or is it Solana-only?
- What's the fee structure? Fixed fee per stream or % of tokens?
- How does auto-claim work — does it push tokens or require recipient action?
- Is the STREAM token required to use the platform or just for governance/staking?

## Sources
- https://streamflow.finance/
- https://streamflow.finance/vesting
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
