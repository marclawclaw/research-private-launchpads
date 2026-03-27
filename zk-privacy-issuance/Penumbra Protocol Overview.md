---
topic: Penumbra Protocol
type: competitor
tags: [penumbra, cosmos, ibc, shielded-pool, privacy, zk, pos]
confidence: high
last_updated: 2026-03-27
sources:
  - https://penumbra.zone/
  - https://protocol.penumbra.zone/main/index.html
  - https://github.com/penumbra-zone/penumbra
---

## Summary
Penumbra is a fully private proof-of-stake network and DEX for the Cosmos/IBC ecosystem. It uses a multi-asset shielded pool (based on Zcash Sapling design) so that all value — including staking, trading, and governance — is private by default. Assets from any IBC-compatible chain can be shielded by depositing into Penumbra.

## Key Facts
- **Architecture:** Standalone Cosmos SDK chain; all transactions private (no transparent pool)
- **Privacy model:** Multi-asset shielded pool; ZK proofs generated client-side on user devices (ultralight nodes)
- **Proof system:** ZK-SNARKs (Zcash Sapling inspired)
- **IBC integration:** Inbound IBC transfers shield assets; outbound IBC transfers unshield — entire Cosmos ecosystem acts as Penumbra's "transparent zone"
- **No accounts:** Only validators have long-term identity; users interact through notes/UTXOs
- **DEX:** ZSwap — supports sealed-bid batch auctions (prevents frontrunning) and Uniswap-v3-style concentrated liquidity; liquidity positions created anonymously
- **Staking (private):** Delegation tokens represent validator shares, recorded in the shielded pool — first-class staking derivatives; exchange rate mechanism replaces explicit staking rewards
- **Governance:** Secret ballots — voters prove ownership of bonded stake without revealing identity; votes encrypted to threshold key
- **Selective disclosure:** Users can reveal transaction details to chosen parties for accounting/compliance
- **Current metrics (2026):** ~$3.77M TVL, $3.77M 30-day DEX volume, 6 connected chains; $11K TVL per some 2025 analyses (discrepancy likely due to measurement time)
- **Wallet:** PRAX wallet extension (browser); CLI tool: `pcli`
- **Docs:** guide.penumbra.zone, protocol.penumbra.zone, rustdoc.penumbra.zone

## How it relates to Logos
- Penumbra's sealed-bid batch auction DEX is directly applicable to private token sale mechanics — bids are hidden, price discovery happens without revealing individual strategies
- The shielded pool model (inbound = shield, outbound = unshield) is a clean design for a cross-chain private launchpad: raise on any IBC chain, settle privately in Penumbra
- Delegation tokens as first-class shielded assets demonstrates that even protocol-native token issuance (staking derivatives) can be fully private
- Logos could study Penumbra's selective disclosure mechanism for compliance-compatible private issuance

> [!analysis] Penumbra is more mature than Aztec on mainnet but niche — low TVL, Cosmos-only IBC connectivity. Its sealed-bid DEX is uniquely relevant for private token sales.

> [!fact] Penumbra has no transparent pool at all — the entire chain is shielded. This is a more radical privacy stance than Aztec (which supports hybrid public/private state).

## Open Questions
- Does Penumbra support arbitrary token issuance (e.g., new project launching its token), or only IBC-bridged assets?
- What are ZK proof generation times on client devices for typical transactions?
- Is there an SDK or programmatic API for building launchpad-style applications on Penumbra?
- What are regulatory risks for Penumbra given the "no transparent pool" stance?

## Sources
- https://penumbra.zone/
- https://protocol.penumbra.zone/main/index.html
- https://github.com/penumbra-zone/penumbra
- https://buf.build/penumbra-zone/penumbra
