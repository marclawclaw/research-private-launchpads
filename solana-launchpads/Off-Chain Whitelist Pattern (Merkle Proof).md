---
topic: Solana Token Launchpads & Permissioned Sales
type: concept
tags: [solana, whitelist, merkle-proof, permissioned, anchor, off-chain]
confidence: high
last_updated: 2026-03-27
sources:
  - https://github.com/palsp/solana-launchpad
  - https://github.com/Alfie/solana-merkle-proof-whitelist
  - https://github.com/sayantank/anchor-whitelist
---

# Off-Chain Whitelist Pattern (Merkle Proof)

## Summary
The dominant pattern for permissioned Solana token sales uses an off-chain Merkle tree of allowed wallet addresses. The on-chain program verifies a Merkle proof during purchase, confirming that the buyer's address is in the whitelist without storing the full list on-chain. This keeps permissioning cheap and scalable.

## Key Facts
- **Implementation reference:** `palsp/solana-launchpad` (Anchor Framework) — inspired by `anchor/tests/ido-pool` and `sayantank/anchor-whitelist`
- **How it works:**
  1. Organizer collects whitelisted wallet addresses off-chain
  2. Computes Merkle root from the list; stores root on-chain in program state
  3. At purchase time, buyer submits their Merkle proof alongside the transaction
  4. On-chain program verifies proof against stored root — O(log n) verification
- **Trust model:** Merkle root integrity guaranteed on-chain; list construction is off-chain and must be trusted
- Scales to thousands of addresses with minimal on-chain storage (just 32 bytes for the root)
- Alternative: `Alfie/solana-merkle-proof-whitelist` — standalone gating primitive for composing with other contracts
- Built with Anchor Framework (Rust), deployed to Solana devnet/localnet for testing

> [!fact] Confirmed from GitHub README and repo structure
> palsp/solana-launchpad is a community reference implementation, not audited production code

> [!analysis] The off-chain list construction is the trust gap — whoever builds the Merkle tree controls access. For trustless permissioning (e.g., KYC attestations, NFT gating), a verifiable on-chain credential source is needed.

## How it relates to Logos
- Merkle proof whitelist is a practical short-term pattern for a Logos private launchpad — simple, gas-efficient
- Long-term, Logos could replace the off-chain list with Waku-attested credentials or Codex-stored KYC attestations
- The on-chain verification step could incorporate a Logos ZK credential proof instead of a static list

## Open Questions
- How are whitelists updated if addresses need to be added/removed post-deployment?
- How does this interact with Solana Token-2022 Transfer Hooks — could hooks enforce whitelist membership on every transfer?
- Is there a way to tie Merkle leaf data to identity attributes (not just addresses)?

## Sources
- https://github.com/palsp/solana-launchpad
- https://github.com/sayantank/anchor-whitelist
- https://github.com/Alfie/solana-merkle-proof-whitelist
