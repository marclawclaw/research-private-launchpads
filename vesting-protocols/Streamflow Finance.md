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

## Fee Structure

> [!fact] Confirmed from Streamflow official docs (docs.streamflow.finance/costs-of-using-streamflow)

- **Platform fee (issuer):** Flat SOL fees per action (not percentage-based):
  - Vesting/Lock/Escrow creation: 0.16 SOL (~$20-25) per contract + 0.0147 SOL network fee
  - Auto-Claim add-on: 0.25 SOL per contract
  - Staking Pool creation: 1.30 SOL (~$160-200) per pool
  - Custom Oracle Infrastructure: minimum 0.13 SOL + 0.000078 SOL per unlock
- **Participant fee (buyer/recipient):**
  - Airdrop claim: 0.009-0.017 SOL (~$1-2) per claim + network fees
  - Airdrop clawback: 1.70% of total tokens returned + network fees
- **Listing/setup fee:** None beyond the per-contract creation fees listed above
- **Staking requirement:** STREAM token is stakeable for rewards but NOT required to use the platform
- **Gas/proof costs:** Solana network fees (~0.0147 SOL per transaction). Minimal compared to EVM alternatives
- **Sybil Checker:** 0.12 USDC per wallet address checked (via CSV upload)
- **Revenue model:** (1) Flat per-contract creation fees, (2) airdrop claim fees, (3) clawback percentage fees (1.70%), (4) protocol fees allocated to STREAM token reward system, (5) custom enterprise pricing available

> [!analysis] Streamflow's flat-fee model (SOL-denominated, not percentage-based) makes it extremely cheap for large token distributions. A project vesting tokens to 100 recipients pays ~16 SOL ($2,000-2,500) total in Streamflow fees — compared to thousands in EVM gas fees for equivalent Sablier operations. The 1.70% clawback fee is the only percentage-based charge. Streamflow is the most cost-effective vesting solution for Solana-native projects.

## Sale Lifecycle & Close Mechanics

> [!fact] Confirmed from Streamflow official docs (docs.streamflow.finance/cancel-contract) and platform behavior

- **Manual close (issuer):** Yes — **contract cancellation is a configurable feature**. When creating a vesting contract, the sender (issuer) can configure cancellation permissions. If enabled, the sender can cancel the contract at any time — including while it is active or before it has started. Cancellation can be granted to: (a) sender only, (b) recipient only, or (c) either party.
- **Automatic close triggers:** (1) **Vesting schedule completion** — all tokens fully unlocked and available to claim; the contract naturally concludes. (2) **Auto-claim at unlock** — if auto-claim is configured, tokens are pushed to the recipient at each unlock event. No documented automatic early-termination triggers.
- **Emergency halt/pause:** Not directly documented as a "pause" function. Cancellation is the primary intervention mechanism. The sender can cancel a scheduled (not-yet-started) contract as well as an active one. There is no mid-stream "pause" that suspends vesting temporarily without cancellation. Streamflow platform-level controls: the platform could theoretically halt operations, but no emergency halt function is documented at the contract level.
- **Admin override:** Limited. Streamflow deploys the contracts, but the cancellation rights are configured by the sender at creation. The Streamflow platform does not appear to have an admin override to cancel contracts on behalf of issuers. Each contract's cancellation authority is determined by its creation parameters.
- **Resume after pause:** Not applicable — there is no pause mechanism. If a contract is cancelled, it cannot be uncancelled. A new contract must be created to resume vesting.
- **Post-close behavior:** On cancellation:
  - All **unlocked (vested) tokens** are transferred to the recipient immediately
  - All **remaining locked tokens** are returned to the sender
  - The contract is permanently terminated — no further vesting
  - On natural completion: recipient can claim all vested tokens; auto-claim pushes tokens automatically if configured
  - **Clawback fee:** If tokens are returned via cancellation of an airdrop (clawback), Streamflow charges **1.70% of total tokens returned**
- **Enforcement:** On-chain (Solana smart contract). Cancellation is a smart contract transaction — the program enforces the split of vested vs. unvested tokens at cancellation time. The cancellation permission (who can cancel) is stored on-chain in the contract state. FYEO and OPCODES audits confirm the on-chain enforcement. Multi-chain support (Solana primary, EVM secondary) means enforcement is chain-specific.

> [!analysis] Streamflow's cancellation model is a clawback mechanism for issuers (e.g., team member departure, failed project milestone) rather than an investor protection feature. The configurable permission model (sender-only, recipient-only, or either) gives flexibility — a DAO could configure recipient-cancellable contracts (allowing recipients to exit early), while a team vesting contract would be sender-only. The 1.70% clawback fee on airdrop returns is a notable cost consideration for large-scale cancellations.

## Open Questions
- Does Streamflow support EVM chains or is it Solana-only?
- What's the fee structure? Fixed fee per stream or % of tokens?
- How does auto-claim work — does it push tokens or require recipient action?
- Is the STREAM token required to use the platform or just for governance/staking?

## Sources
- https://streamflow.finance/
- https://streamflow.finance/vesting
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
