---
topic: Penumbra ZSwap DEX
type: concept
tags: [penumbra, dex, sealed-bid, batch-auction, concentrated-liquidity, privacy]
confidence: high
last_updated: 2026-03-27
sources:
  - https://protocol.penumbra.zone/main/index.html
  - https://penumbra.zone/blog/shielded-staking-on-penumbra
---

## Summary
ZSwap is Penumbra's private DEX combining sealed-bid batch auctions with Uniswap-v3-style concentrated liquidity. Trades are fully private; only net flow across an asset pair is revealed per block, preventing frontrunning and MEV while enabling efficient price discovery.

## Key Facts
- **Two execution modes:**
  1. **Sealed-bid batch auctions** — orders submitted encrypted; entire batch executes at a uniform clearing price; only net flow per pair revealed per block
  2. **Concentrated liquidity** — Uniswap-v3 style; liquidity positions created anonymously; LPs set their own fees
- **MEV prevention:** Sealed-bid model eliminates sandwich attacks and frontrunning by design
- **Privacy of LP positions:** Liquidity positions are just notes in the shielded pool — LPs don't reveal their beliefs about prices
- **Revelation model:** Per-block net flow (aggregate) is public; individual order sizes/directions are private
- **Selective disclosure:** Traders can reveal their own trade history to third parties (e.g., for tax compliance)

## How it relates to Logos
- Sealed-bid batch auctions are the ideal mechanism for private token launches: participants submit bids privately, a clearing price is computed, tokens are distributed — no one can front-run or extract MEV
- This is a concrete reference implementation for the "private token sale" use case — not theoretical
- A Logos-based launchpad could adopt the sealed-bid batch auction model either natively or by routing through Penumbra via IBC

> [!analysis] ZSwap's sealed-bid auction is the most privacy-preserving token distribution mechanism found in this research. It directly solves the front-running problem in token launches.

## Open Questions
- What is the latency of a sealed-bid auction cycle? (Minimum time from bid to token receipt)
- Is ZSwap's clearing price mechanism audited and formally verified?
- Can ZSwap be used for initial token issuance (not just secondary trading)?

## Sources
- https://protocol.penumbra.zone/main/index.html
- https://penumbra.zone/
