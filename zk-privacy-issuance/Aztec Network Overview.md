---
topic: Aztec Network
type: competitor
tags: [aztec, zk, ethereum, l2, privacy, token-issuance]
confidence: high
last_updated: 2026-03-27
sources:
  - https://aztec.network/basics
  - https://aztec.network/blog/
  - https://github.com/AztecProtocol/aztec-packages
---

## Summary
Aztec is a privacy-first Ethereum L2 that enables fully programmable private smart contracts using zero-knowledge proofs. It uses the Noir DSL and the Aztec.nr framework to allow developers to write contracts with both public and private state, including private token issuance and transfers.

## Key Facts
- **Architecture:** Ethereum L2 rollup with hybrid public/private execution
- **Language:** Noir (ZK DSL) + Aztec.nr smart contract framework
- **Prover backend:** Barretenberg (ZK prover, also houses Aztec VM)
- **Current status (2026):** Alpha network live on Ethereum Mainnet at ~1 TPS, ~6s block times; decentralized sequencing and proving active
- **Roadmap phases:**
  - Ignition: governance + block building validation on Mainnet (done)
  - Alpha: 1 TPS, 6s blocks, bug bounty, ongoing audits (current)
  - Beta: >10 TPS, reduced block times, 99.9% uptime, no critical bugs in 3 months
- **TGE:** Earliest February 11, 2026; community vote required
- **Token auction:** Public auction ran Dec 2–6, 2025
- **TVL:** ~$8.74M (per 2025 analysis)
- **Governance:** AZIP/AZUP system — on-chain sequencer signaling + tokenholder supermajority vote; no central team control
- **Packages:** barretenberg (prover), l1-contracts (Solidity rollup), noir-projects (Noir circuits + contracts), yarn-project (TS client/backend), Aztec.js (SDK), PXE (Private Execution Environment)

## How it relates to Logos
- Aztec's programmable privacy model is the strongest Ethereum-native analogue to what a Logos-based private launchpad might need
- The AZIP/AZUP governance model (sequencer signaling + tokenholder vote) is a reference design for decentralized upgrade processes
- Aztec's hybrid public/private function execution is directly relevant to token sale contracts where some state (e.g. total supply) is public, but buyer identities are private
- Logos could build analogous privacy primitives or integrate with Aztec for Ethereum-side token distribution

> [!analysis] Aztec is the most technically mature ZK private contract platform as of early 2026, but still early-Alpha with limited TPS. Ecosystem applications are nascent.

## Open Questions
- When does Aztec reach Beta / production-grade TPS?
- Are there production private token sale contracts (beyond examples) deployed on Alpha?
- What are actual proof generation times/costs for token issuance contracts?
- Does Aztec support selective disclosure for regulatory compliance?

## Sources
- https://aztec.network/basics
- https://aztec.network/blog/
- https://aztec.network/roadmap
- https://github.com/AztecProtocol/aztec-packages
- https://www.bankless.com/read/privacy-l2-aztec-is-almost-ready-for-primetime
