---
topic: ZK Token Issuance Patterns
type: analysis
tags: [zk, token-issuance, private-launchpad, aztec, penumbra, design-patterns]
confidence: medium
last_updated: 2026-03-27
sources:
  - https://aztec.network/basics
  - https://protocol.penumbra.zone/main/index.html
  - https://www.cache256.com/ecosystem/shielded-pools-defi-privacy-infrastructure-analysis/
---

## Summary
ZK-based token issuance can be implemented through two main patterns: (1) programmable private contracts (Aztec model — flexible, EVM-compatible) and (2) shielded pool ingestion via protocol-defined mechanisms (Penumbra model — simpler, IBC-native). Both support private buyer identity but differ in flexibility, ecosystem reach, and maturity.

## Key Facts

### Pattern 1: Aztec Programmable Private Contracts
- **How it works:** Deploy a private smart contract in Noir/Aztec.nr; define mint, transfer, and access-control logic; buyers generate ZK proofs of eligibility client-side via PXE; tokens issued as private notes
- **Advantages:** Fully programmable (whitelist logic, vesting, conditional minting); Ethereum-native (L2); composable with public contracts
- **Limitations:** Alpha-stage, ~1 TPS; proof generation overhead; small developer ecosystem
- **Use for launchpad:** Mint private allocation notes conditioned on ZK proof of eligibility (e.g., proof of KYC attestation without revealing identity)

### Pattern 2: Penumbra Shielded Pool + IBC
- **How it works:** Issue token on any IBC-compatible chain; route it via IBC into Penumbra — it becomes a shielded asset; distribute via sealed-bid batch auction (ZSwap)
- **Advantages:** Leverages existing IBC ecosystem; sealed-bid auction prevents front-running; works with any IBC token (not just Penumbra-native)
- **Limitations:** Cosmos/IBC only; limited programmability for custom sale logic; Penumbra has no accounts (complicates KYC-style gating)
- **Use for launchpad:** IBC asset → Penumbra shielded pool → ZSwap sealed-bid auction → private allocation

### Pattern 3: Shielded Pool Add-On (Railgun model, reference)
- **How it works:** Wrap existing EVM tokens with a shielded pool; relayers execute transactions; no new chain required
- **Advantages:** Works with any EVM token; integrates with existing DeFi
- **Limitations:** Not programmable for issuance logic; more of a "private transfer" layer than issuance mechanism

## How it relates to Logos
- For a Logos-based private launchpad, **Pattern 1 (Aztec)** is the right long-term architecture: programmable, composable, Ethereum-bridgeable
- **Pattern 2 (Penumbra)** is viable for a Cosmos-ecosystem launchpad today — more practical near-term if targeting IBC chains
- The key gap in both: no mature, production-ready private token sale contract exists off-the-shelf; both require custom development
- Logos could differentiate by building a reusable private launchpad contract on Aztec.nr with selective disclosure hooks for compliance

> [!analysis] Neither Aztec nor Penumbra has a production private launchpad product. This is an open build opportunity. Aztec has the contract primitives; Penumbra has the auction mechanism.

## Open Questions
- Can ZK proof of eligibility (e.g., accredited investor status) be combined with private token receipt in Aztec without a trusted third party?
- Is there any existing private launchpad contract in the Aztec or Penumbra ecosystems?
- What is the minimum trust assumption for each pattern? (Trusted setup? Relayer honesty?)

## Sources
- https://aztec.network/basics
- https://aztec.network/blog/introducing-aztec-nr-aztecs-private-smart-contract-framework
- https://protocol.penumbra.zone/main/index.html
- https://www.cache256.com/ecosystem/shielded-pools-defi-privacy-infrastructure-analysis/
