---
topic: Token Vesting & Distribution Protocols
type: competitor
tags: [vesting, streaming, EVM, Solana, DeFi, protocol]
confidence: high
last_updated: 2026-03-27
sources: [https://sablier.com/, https://github.com/sablier-labs/evm-monorepo]
---

## Summary
Sablier is the leading token streaming and vesting protocol, live since 2019. It enables per-second token vesting via smart contracts across 27 EVM chains and Solana. Its key innovation is treating vesting as a continuous real-time stream rather than periodic discrete unlocks.

## Key Facts
- **Founded:** 2019 — battle-tested, longest-running vesting protocol
- **Chains:** 27 EVM chains + Solana (Ethereum, Arbitrum, Base, Polygon, Optimism, BSC, Avalanche, Berachain, etc.)
- **Investors:** a16z crypto, A Capital, Factor, Gd1, Fenbushi
- **Architecture:** EVM monorepo with 4 protocol packages:
  - `lockup` — fixed-term vesting and token distribution
  - `flow` — open-ended streaming with no fixed end time
  - `airdrops` — Merkle-based token distribution with optional vesting
  - `bob` — price-gated vaults with optional yield adapters
- **Schedules supported:** Linear, cliff, monthly unlocks, discrete unlocks, timelocks, custom curves
- **Bulk streams:** Create hundreds of streams at once via CSV upload
- **Security:** Multiple audits (Cantina, Codehawks, 5+ other auditors); bug bounty program
- **License:** BSL 1.1 (v2), transitioning to open source after grace period
- **Permissionless:** No gatekeepers, pure DeFi

## Technical Architecture
- `SablierLockup` contract family: `LockupLinear`, `LockupDynamic`, `LockupTranched`
- NFT-based stream ownership — streams are transferable ERC-721 tokens
- Recipients can withdraw streamed funds at any time without sender involvement
- Streams can be canceled (revocable) or made permanent
- Airdrops use Merkle trees for gas-efficient batch claiming with optional vesting

> [!fact] Confirmed from official docs
> Sablier has been live since 2019 and is used by top organizations including Uniswap, Optimism, and others.

## How it relates to Logos
- Gold standard reference for vesting protocol design; any Logos launchpad should study Sablier's architecture
- The NFT-as-stream-ownership model is elegant — transferable vesting positions have secondary market value
- Multi-chain deployment pattern (same contracts, different chains) is a template for Logos ecosystem expansion
- `flow` (open-ended streaming) is interesting for continuous contributor payments in DAO contexts

## Fee Structure

> [!fact] Confirmed from Sablier official docs (docs.sablier.com/concepts/protocol/fees) and blog post "Why and How Sablier Is Still Free to Use" (Nov 2024)

- **Platform fee (issuer):** Zero — "The Sablier Protocol is entirely free to use. There is no protocol fee." This is confirmed as of late 2024
- **Participant fee (buyer/recipient):** Zero — no fees charged by Sablier for creating, claiming, or withdrawing from streams
- **Broker fee (third-party integrators):** External front-end operators MAY charge a broker fee (0-10% of streamed amount) when users create streams through their interfaces. The official Sablier interface does NOT charge broker fees. This is an optional monetisation mechanism for third-party builders
- **Listing/setup fee:** None
- **Staking requirement:** None — Sablier has no native token. The protocol is fully permissionless
- **Gas/proof costs:** Standard EVM gas fees for creating streams, withdrawing funds, and claiming airdrops. Gas costs vary significantly by chain (Ethereum mainnet = expensive; L2s like Arbitrum/Base = cheap). Merkle-based airdrops are gas-efficient for batch distribution
- **Revenue model:** Sablier does not extract protocol-level fees. Revenue model is based on: (1) VC funding (a16z crypto, A Capital, etc.), (2) potential future protocol fee that can be enabled by governance, (3) broker fee system incentivises third-party integrations (ecosystem growth), (4) BSL 1.1 license protects commercial interests. Sablier is "free now" but has a governance-activatable fee switch

> [!analysis] Sablier is the only completely free protocol in this comparison — zero fees at every level. This is a deliberate strategy to maximise adoption and build network effects before potentially activating fees later (similar to Uniswap's fee switch). For projects choosing between vesting solutions, Sablier's zero-fee model is unbeatable on cost — the only expense is gas. However, EVM gas costs on Ethereum mainnet can be significant for large-scale distributions, making Streamflow (Solana-native) or Sablier-on-L2s more cost-effective for high-volume use cases.

## Sale Lifecycle & Close Mechanics

> [!fact] Confirmed from Sablier official docs (docs.sablier.com/concepts/cancelability, docs.sablier.com/concepts/flow/overview) and GitHub repo

- **Manual close (issuer):** Yes — **cancelability is a first-class feature, set at stream creation**:
  - **Lockup streams (cancelable):** The stream creator can cancel at any time. Unstreamed (unvested) funds are returned to the creator; already-streamed tokens remain claimable by the recipient. Cancellation is immediate and irrevocable.
  - **Lockup streams (non-cancelable):** Cannot be cancelled by anyone — the recipient is guaranteed to receive all funds. Making a cancelable stream non-cancelable is a one-way operation (irreversible). A non-cancelable stream cannot be made cancelable again.
  - **Recipients cannot cancel** — only the stream creator holds cancel rights on Lockup streams.
  - **Flow streams:** Do not have a "cancel" function per se; they have pause, restart, and void operations instead.
- **Automatic close triggers:** (1) **Stream end time reached** — Lockup streams have a fixed end time after which all tokens are fully vested and claimable. (2) **All tokens withdrawn** — once the recipient withdraws all streamed tokens, the stream is functionally complete. No documented hardcap or external trigger.
- **Emergency halt/pause:**
  - **Lockup streams:** No pause mechanism — only cancel (permanent) or the creator can stop funding. Once deployed, a cancelable stream can be cancelled instantly.
  - **Flow streams:** Full pause/restart cycle supported. The sender can pause a Flow stream at any time; previously accrued debt is preserved. The sender can restart a paused stream. **Void** is the permanent termination — either party can void a Flow stream, making it non-restartable. Voiding an insolvent stream forfeits uncovered debt.
  - **Merkle airdrops:** Creator can recover unclaimed funds (a) before any claims, (b) up to 7 days after first claim, (c) after claim window ends (if configured). After the 7-day window and without a claim end date, unclaimed funds are permanently locked.
- **Admin override:** None — Sablier is a fully permissionless protocol. There is no admin key, no multisig, no pause guardian. The protocol team (Sablier Labs) cannot intervene in individual streams. "No gatekeepers, pure DeFi."
- **Resume after pause:** 
  - **Flow streams:** Yes — paused streams can be restarted by the sender. Accrued debt is preserved through pause/restart cycles.
  - **Lockup cancelled streams:** No — cancellation is permanent. A new stream must be created.
  - **Voided Flow streams:** No — void is permanent and irreversible.
- **Post-close behavior:**
  - On cancellation of Lockup: unstreamed tokens returned to creator; streamed tokens remain in protocol for recipient to withdraw at will (no expiry on withdrawal rights).
  - On stream end: all tokens are streamed; recipient can withdraw at their convenience (no expiry).
  - On void of Flow: stream stops accruing; any debt owed to recipient that was covered remains withdrawable; uncovered insolvent debt is forfeited.
  - NFT-based ownership: Lockup streams are ERC-721 NFTs owned by the recipient — the stream position can be transferred or sold on secondary markets.
- **Enforcement:** On-chain (smart contract, 27 EVM chains + Solana). All cancelability, pause, restart, and void operations are smart contract functions. The cancelable/non-cancelable flag is immutable once set (except the one-way conversion from cancelable → non-cancelable). Multiple audits (Cantina, Codehawks, 5+ others) confirm the on-chain enforcement. Zero admin keys = zero platform-level override capability.

> [!analysis] Sablier offers the most nuanced cancel/pause mechanics of any vesting protocol studied. The distinction between Lockup (cancel = immediate termination) and Flow (pause/restart/void) reflects two different use cases: Lockup is for structured vesting with defined endpoints; Flow is for ongoing streaming payments. The one-way cancelable → non-cancelable conversion is an elegant trust mechanism — projects can commit to non-revocable vesting as a credible signal to investors, but only by giving up the flexibility to clawback. The complete absence of admin keys is the key differentiator from Streamflow and Hedgey.

## Open Questions
- Does Sablier have a permissioned/private mode where allocations are not publicly visible?
- What are the fee structures — does Sablier take a protocol fee?
- Is the Solana implementation feature-parity with EVM?
- How does Sablier handle cross-chain vesting scenarios?

## Sources
- https://sablier.com/
- https://github.com/sablier-labs/evm-monorepo
- https://docs.sablier.com/concepts/lockup
