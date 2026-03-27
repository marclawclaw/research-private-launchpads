---
topic: Token Sale Permissioning Mechanisms
type: concept
tags: [ethereum, permissioned, allowlist, whitelist, kyc, merkle-proof, sybil-resistance]
confidence: high
last_updated: 2026-03-27
sources:
  - https://www.cube.exchange/what-is/allowlistblocklist
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
  - https://coinmarketcap.com/alexandria/article/what-is-dao-maker
---

## Summary
Ethereum token sales use several complementary permissioning mechanisms to restrict participation. These range from simple address-based allowlists to token stake requirements, KYC, and ZK-proof-based identity attestations. Each trades off decentralisation, privacy, and Sybil resistance differently.

## Key Facts

### Mechanism Types

| Mechanism | How it works | Sybil resistance | Privacy |
|-----------|-------------|-----------------|---------|
| Address allowlist (Merkle proof) | Off-chain list → on-chain Merkle root; user provides proof at claim | Low (easy to multiply wallets) | High |
| Token stake (e.g. POLS, $DAO) | Hold/stake platform token for N days to qualify | Medium (economic cost) | High |
| KYC + wallet binding | Identity verified off-chain, wallet address registered | High | Low |
| ZK-proof KYC | User proves KYC membership without revealing identity | High | High |
| Lottery + stake | Stake determines ticket count; winner drawn randomly | Medium | Medium |

### Implementations in the wild
- **[[Fjord Foundry]]**: Optional project-managed whitelist (address-based); no platform-level token gate
- **[[DAO Maker]]**: $DAO stake → tier → guaranteed allocation; centralised KYC mandatory
- **[[Polkastarter]]**: $POLS stake/hold 7 days → POLS Power → lottery ticket count per IDO
- **ZK approach** (emerging): ZK proofs allow proving KYC membership without on-chain address exposure (e.g. Cube Exchange references)

### On-chain enforcement patterns
- **Merkle proof allowlist**: Most common — gas efficient, requires off-chain list management
- **ERC-20 balance check**: Simple but Sybil-vulnerable without time lock
- **Staking contract + snapshot**: Time-locks tokens, creates commitment; more robust
- **Signature-based** (off-chain KYC → signed claim): Centralised but flexible

## How it relates to Logos
- Logos' privacy stack could enable ZK-proof-based permissioning (prove eligibility without revealing identity)
- A Logos launchpad could use Waku/Nomos for off-chain allowlist coordination + on-chain Merkle root for enforcement
- The gap between current state (KYC-centralised or stake-plutocratic) and privacy-preserving permissioning is a clear product opportunity

> [!analysis] ZK-based allowlist is technically feasible today (via Semaphore, ZK-KYC protocols) but not yet mainstream on Ethereum launchpads — first-mover opportunity

## Open Questions
- Which ZK identity protocols (Semaphore, Worldcoin, Polygon ID) are practical for launchpad gating today?
- Can Logos' Nomos/Waku be used for off-chain allowlist coordination without a centralised server?

## Sources
- https://www.cube.exchange/what-is/allowlistblocklist
- https://coinmarketcap.com/alexandria/article/what-is-dao-maker
