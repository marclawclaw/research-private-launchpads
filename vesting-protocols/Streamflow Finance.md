---
topic: Token Vesting & Distribution Protocols
type: competitor
tags: [vesting, streaming, Solana, distribution, airdrops, payroll]
confidence: high
last_updated: 2026-04-02
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

## Refund & Participant Protection

> [!fact] Cancellation mechanics confirmed from Streamflow documentation (docs.streamflow.finance)

- **Refund window:** Not applicable — Streamflow is a vesting/distribution platform, not a token sale platform. There is no "purchase" to refund.
- **Minimum raise threshold (soft cap):** Not applicable — Streamflow does not conduct token sales.
- **Post-launch performance refund:** Not applicable.
- **Cancellation rights:** Yes — **vesting contract cancellation is a configurable feature.** When creating a vesting contract, the sender can set cancellation rules. If cancelled: all unlocked (vested) tokens are transferred to the recipient, and all remaining locked tokens are returned to the sender. This is an issuer-side control, not an investor-initiated refund right.

> [!analysis] Streamflow's cancellation feature is a *clawback* mechanism for issuers (e.g., if a team member leaves), not a refund mechanism for investors. Investors/recipients cannot unilaterally cancel a vesting contract and reclaim their original payment — they only receive what has already vested. This is fundamentally different from DAO Maker's DYCO refund model.

## Open Questions
- Does Streamflow support EVM chains or is it Solana-only?
- What's the fee structure? Fixed fee per stream or % of tokens?
- How does auto-claim work — does it push tokens or require recipient action?
- Is the STREAM token required to use the platform or just for governance/staking?

## Sources
- https://streamflow.finance/
- https://streamflow.finance/vesting
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
