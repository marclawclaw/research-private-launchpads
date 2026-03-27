---
topic: Aztec.nr Framework
type: concept
tags: [aztec, noir, smart-contracts, private-state, token-issuance]
confidence: high
last_updated: 2026-03-27
sources:
  - https://aztec.network/blog/introducing-aztec-nr-aztecs-private-smart-contract-framework
  - https://github.com/AztecProtocol/aztec-packages
---

## Summary
Aztec.nr is a smart contract framework built on top of Noir that adds blockchain semantics (addresses, msg.sender, state, events, cross-chain messaging) to the base ZK language. It provides high-level note management abstractions for private state, removing the need for developers to manually implement Merkle trees and nullifiers.

## Key Facts
- **Base language:** Noir (universal ZK programming language, developed by Aztec Labs)
- **What Aztec.nr adds over vanilla Noir:**
  - Contracts with addresses and callable functions
  - Inter-contract calls
  - Persistent state variables
  - `msg.sender` and call context
  - Historic blockchain access
  - Encrypted and unencrypted events/logs
  - Cryptographic primitives
  - Cross-chain L1↔L2 message passing
- **Private state model:** UTXO-style notes — each note is a value owned by an address, managed via Merkle trees and nullifiers
- **Key note primitives:** `get_balance`, `increment`, `decrement`, `decrement_by_at_most` — abstractions over note aggregation, nullification, and change creation
- **Example contracts in repo:**
  - `private_token_contract` — canonical private token with shielded balances
  - `uniswap_contract` — private swap
  - `lending_contract` — private lending
- **Private Execution Environment (PXE):** Client-side component that generates ZK proofs locally before submitting to the network; Aztec.js communicates through PXE

## How it relates to Logos
- Aztec.nr's note abstraction is a direct template for how a Logos-side private token launchpad contract could manage anonymous purchase receipts and allocation proofs
- The `private_token_contract` example demonstrates how token balances can be fully shielded while still enabling transfer and accounting
- PXE's client-side proving is key to the UX model: proofs are generated on the user's device, not revealed to any server

> [!fact] Aztec.nr is production-ready for Alpha network. The private token contract is a first-class example in the official repo.

## Open Questions
- Does Aztec.nr support conditional (gated) private minting — i.e., only mint if a private proof of eligibility is satisfied?
- Is there a private whitelist primitive or equivalent access control for launchpad use?
- What is the note storage cost (gas equivalent) per private allocation?

## Sources
- https://aztec.network/blog/introducing-aztec-nr-aztecs-private-smart-contract-framework
- https://github.com/AztecProtocol/aztec-packages/blob/master/yarn-project/noir-projects/aztec-nr
- https://github.com/AztecProtocol/aztec-packages/blob/master/yarn-project/noir-projects/noir-contracts
