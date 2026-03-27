---
topic: Solana Token Launchpads & Permissioned Sales
type: summary
tags: [solana, launchpad, IDO, ecosystem, pump-fun, magic-eden, daos-fun]
confidence: high
last_updated: 2026-03-27
sources:
  - https://solanacompass.com/projects/category/community/launchpads
  - https://cryptonews.com/cryptocurrency/best-solana-launchpads/
---

# Solana Launchpad Ecosystem Overview

## Summary
Solana's launchpad landscape has bifurcated into two tracks: (1) permissionless memecoin launchpads (Pump.fun) optimizing for zero-friction token creation via bonding curves, and (2) structured/vetted IDO launchpads (Magic Eden Launchpad, DAOs.fun, Solster) that offer whitelist management, multi-phase minting, and vetting. No dominant permissioned/private launchpad exists for institutional or KYC-gated sales.

## Key Facts

### Major platforms (as of 2026)

| Platform | Model | Permissioning | Notes |
|----------|-------|---------------|-------|
| **Pump.fun** | Bonding curve, anyone can launch | None (permissionless) | 0.01 SOL to launch; viral memecoin focus |
| **Magic Eden Launchpad** | Vetting + whitelist mgmt + dynamic pricing | Whitelist (manual) | Large user base; NFT+token launches |
| **DAOs.fun** | Fixed-price fair launch for investment DAOs | No pre-allocation | Auto liquidity bootstrap, 10% to LP |
| **Solster** | Tiered staking for guaranteed allocation | Stake-based tier system | Lottery + guaranteed pools |
| **solana-labs/launchpad** | Reference impl, dynamic pricing | None native | SPL library, not a product |

### Pricing models in use
- **Bonding curve** (Pump.fun): price increases as supply is bought
- **Fixed price** (DAOs.fun, many IDOs): set price, FCFS or lottery allocation
- **Dutch auction** / LBP: price decreases over time (more common on Ethereum)
- **Tiered/lottery** (Solster): stakers get weighted chances at allocation

### Whitelist/access approaches
- Manual whitelist lists (Magic Eden, most IDO platforms)
- Stake-to-qualify tiers (Solster, many launchpads)
- NFT gating (hold platform NFT to participate)
- Off-chain Merkle proof (palsp/solana-launchpad pattern)
- Permissionless (Pump.fun)

> [!fact] Pump.fun data from Ledger Academy (Feb 2026) and Solana Compass
> [!analysis] The gap in the market is a launchpad for institutional/accredited private sales with on-chain KYC attestation + vesting — no major Solana platform does this cleanly

## How it relates to Logos
- Logos could occupy the "permissioned + privacy-preserving" niche that doesn't exist in Solana's current ecosystem
- Most Solana launchpads are transparent and permissionless — a Logos launchpad with [[Solana Token-2022 Confidential Transfers]] + KYC attestations would be genuinely novel
- Composability pattern: sale contract + [[Off-Chain Whitelist Pattern (Merkle Proof)]] + [[Streamflow Finance - Token Distribution Platform]] for post-sale vesting

## Open Questions
- Are there any Solana launchpads using Token-2022 confidential transfers for private sale amounts?
- What is the typical fee structure for IDO platforms?
- Which platforms support multi-round raises (seed → private → public)?

## Sources
- https://solanacompass.com/projects/category/community/launchpads
