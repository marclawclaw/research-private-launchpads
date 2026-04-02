---
topic: Batch Auctions and Commit-Reveal Token Sales
type: concept
tags: [batch-auction, commit-reveal, frontrunning, gnosis-auction, cowswap, token-sale, price-discovery, mev]
confidence: high
last_updated: 2026-04-02
sources:
  - https://medium.com/@gnosisPM/introducing-gnosis-auction-ac30232b3595
  - https://docs.molecule.to/bio.xyz/launchpad/batch-auction-mechanics
  - https://protocol.penumbra.zone/main/dex.html
  - https://arxiv.org/pdf/2301.13785
---

## Summary
Batch auctions and commit-reveal schemes are alternative token sale mechanisms that address the front-running and MEV extraction problems of bonding curves. In a batch auction, all bids are collected in a window, sorted, and cleared at a single uniform price — eliminating ordering advantages. Commit-reveal schemes achieve similar anti-frontrunning properties by requiring participants to cryptographically commit to bids before revealing them. Both mechanisms have production deployments, with Gnosis Auction being the most widely used and [[Penumbra ZSwap DEX]] providing a privacy-native sealed-bid batch auction.

## Key Facts

### The Problem: Bonding Curve Front-Running

In a standard bonding curve:
- Each buy transaction executes at the current price and moves the price up
- A sandwich attacker can: (1) buy before a large transaction, (2) let the victim buy at the inflated price, (3) sell at the new higher price
- Bonding curves on transparent chains (Ethereum, Solana) are especially vulnerable because all pending transactions are visible in the mempool
- MEV bots routinely extract value from token launches via front-running, back-running, and sandwich attacks

> [!fact] The Gnosis Auction announcement explicitly states: "The batched time nature of the auctions greatly reduces frontrunning and gas bidding wars, decreasing the amount of extracted value from auctioneers and bidders."

### Mechanism 1: Batch Auction (Gnosis Auction / CowSwap model)

**How it works:**
1. Auctioneer sets: tokens for sale, duration, minimum bid price, bid token (e.g., USDC)
2. Bidders submit **limit orders** during the auction window: `(quantity_desired, max_price_willing_to_pay)`
3. At auction close: bids are sorted by price descending; a clearing price is found such that supply equals demand
4. **All winning bidders pay the same clearing price** — even those who bid higher get the lower clearing price
5. Bidders who bid below clearing price receive a full refund
6. Unsold tokens returned to auctioneer

**Properties:**
- **Uniform clearing price**: No early-buyer advantage; late bids at the same price have equal standing
- **Front-running resistant**: Bids submitted during the window don't affect each other's prices (unlike continuous AMM swaps)
- **Limit order semantics**: Bidders set maximum price; they can never pay more than they committed to
- **Permissionless or allowlisted**: Gnosis Auction supports both open and allowlisted auctions

**Gnosis Auction specifics:**
- Open-source smart contract on Ethereum: `gnosis-auction.eth`
- Launched March 2021; used by multiple DeFi teams for IDOs
- Bidding token: any ERC-20 (typically ETH or USDC)
- Minimum auction duration: configurable
- Bid withdrawal: allowed before auction close in some configurations

> [!fact] Gnosis Auction is fully on-chain and permissionless — any Ethereum team can deploy and execute batch auctions without central curation.

**bio.xyz (Molecule) Batch Auction variant:**
- Used for biotech token sales on bio.xyz launchpad
- Minimum bid: $100 USDC (retail-accessible)
- Clearing price determined after bid window closes
- Tokens distributed pro-rata at clearing price to all winning bidders
- Refunds processed for overbids and non-clearing bids

### Mechanism 2: Commit-Reveal Schemes

**Two-phase structure:**
1. **Commit phase**: Bidder submits `hash(bid_amount, nonce, address)` — the actual bid is hidden on-chain
2. **Reveal phase**: Bidder reveals plaintext `(bid_amount, nonce)`; contract verifies against committed hash
3. **Settlement**: After reveal window, settle at clearing price or process revealed bids

**Properties:**
- Bids are cryptographically hidden during the commit phase — even validators/miners cannot see bid amounts
- Eliminates front-running because the bid value is unknown until after the commit deadline
- Requires two transactions (commit + reveal), increasing UX friction
- Participants who commit but don't reveal can be penalised (forfeiture of deposit) to prevent strategic non-revelation

> [!fact] Commit-reveal is a well-established cryptographic primitive for preventing front-running. It is used in ENS domain registration (FIFS registrar) and was proposed in the Ethereum yellow paper for auction-style consensus mechanisms.

**Limitations of commit-reveal:**
- Does not hide the *existence* of a bid on transparent chains — only the amount
- If all bids are revealed, the information eventually becomes public (coordination risk)
- Requires a reveal deadline — non-revelation by deadline requires penalty mechanism or resolution protocol

### Mechanism 3: Penumbra ZSwap Sealed-Bid Batch Auction

See [[Penumbra ZSwap DEX]] for full details.

> [!fact] Penumbra: "All swaps in each block are executed in a single batch, with a common clearing price, eliminating frontrunning by eliminating the entire concept of intra-block ordering." (Penumbra Winter 2022 Update)

**Key advantages over transparent commit-reveal:**
- Bids are fully private (ZK-encrypted in Penumbra shielded pool) — amount AND existence hidden
- Clearing price computed across the entire block's batch — no ordering games
- Only **net flow** across an asset pair is revealed per block — no individual trade data
- Natively integrated with concentrated liquidity for post-auction trading

**This is the strongest anti-frontrunning design currently in production for a DEX.**

### Comparison: Bonding Curve vs Batch Auction vs Commit-Reveal

| Property | Constant-Product Bonding Curve | Batch Auction (Gnosis) | Commit-Reveal | Penumbra Sealed-Bid |
|---|---|---|---|---|
| Front-running resistance | ❌ Low | ✅ High | ✅ High | ✅✅ Highest |
| Price certainty for buyer | ❌ (slippage) | ✅ (clearing price) | ✅ (limit price) | ✅ (clearing price) |
| Continuous price discovery | ✅ | ❌ (discrete) | ❌ (discrete) | ❌ (per-block) |
| Capital efficiency | ✅ | ✅ | ✅ | ✅ |
| UX simplicity | ✅ | Medium | ❌ (two tx) | Medium |
| Privacy | ❌ None | ❌ None | Partial | ✅✅ Full |
| Permissioning (allowlist) | Overlay | Supported natively | Overlay | Supported |
| Production deployments | Many (pump.fun, Flaunch) | Yes (Gnosis, bio.xyz) | Limited (ENS) | Yes (Penumbra) |

### Production Deployments

| Platform | Mechanism | Chain | Status |
|---|---|---|---|
| Gnosis Auction | Batch auction | Ethereum | Live (open-source) |
| CowSwap | Batch auction (CoW Protocol) | Ethereum, Gnosis Chain | Live |
| bio.xyz (Molecule) | Batch auction | Ethereum | Live |
| Bounce Finance | Multiple (English, Dutch, sealed) | Multi-chain | Live |
| Penumbra ZSwap | Sealed-bid batch | Cosmos/IBC | Live |
| Aztec token launch (2025) | Continuous liquidation auction + ZK passport | Ethereum | Launched Nov 2025 |

> [!fact] The Aztec ($AZTEC) token launch in November 2025 used a Continuous Clearing Auction Protocol (CCA) on Uniswap V4, with ZKPassport's Noir circuits for compliance checks. This is the most recent example of a privacy-aware batch auction for token launches.

## How it relates to Logos

> [!analysis] Batch auctions and commit-reveal schemes are more aligned with Logos' values than constant-product bonding curves for the primary token launch mechanism. They eliminate front-running, provide uniform pricing (fairer distribution), and can support privacy via Penumbra-style sealed bids.

Specific recommendations:
1. **For RFP-015 (bonding curve launchpad)**: A sealed-bid batch auction during the initial launch window followed by a bonding curve for secondary market trading would combine the best properties. The bonding curve handles continuous price discovery post-launch; the batch auction handles the fair initial distribution.
2. **For privacy-preserving launches**: Route through or model after [[Penumbra ZSwap DEX]] sealed-bid mechanism — only net flow is revealed, individual bids are private.
3. **Gnosis Auction contracts are open-source**: Could be forked as a starting point for an on-chain batch auction launchpad on Logos-compatible chains.
4. **Commit-reveal is implementable on any EVM chain** without ZK infrastructure — a simpler path to anti-frontrunning than full ZK sealed bids.

## Open Questions
- Can Penumbra ZSwap's sealed-bid batch auction be adapted for an initial token distribution (not just ongoing DEX trades)?
- What's the minimum viable auction duration for price discovery — is a 24-hour window sufficient, or do batch auctions benefit from longer commitment windows?
- How does Bounce Finance's sealed-bid auction differ from Gnosis Auction mechanically?
- Can commit-reveal be combined with ZK proofs (e.g., ZK-commit: prove bid is within valid range without revealing amount)?
- Is there a hybrid — bonding curve for secondary trading + sealed-bid batch auction for initial distribution — deployed anywhere in production?

## Sources
- https://medium.com/@gnosisPM/introducing-gnosis-auction-ac30232b3595
- https://medium.com/gnosis-pm/announcing-gnosis-auction-launch-390124d56248
- https://docs.molecule.to/bio.xyz/launchpad/batch-auction-mechanics
- https://protocol.penumbra.zone/main/dex.html
- https://penumbra.zone/blog/2022-winter-update
- https://arxiv.org/pdf/2301.13785 (commit-reveal anti-frontrunning paper)
- https://aztec.network/blog/the-ticker-is-aztec
