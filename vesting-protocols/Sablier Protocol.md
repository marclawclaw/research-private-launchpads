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

## Open Questions
- Does Sablier have a permissioned/private mode where allocations are not publicly visible?
- What are the fee structures — does Sablier take a protocol fee?
- Is the Solana implementation feature-parity with EVM?
- How does Sablier handle cross-chain vesting scenarios?

## Sources
- https://sablier.com/
- https://github.com/sablier-labs/evm-monorepo
- https://docs.sablier.com/concepts/lockup
