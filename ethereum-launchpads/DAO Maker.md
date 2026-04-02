---
topic: DAO Maker
type: competitor
tags: [ethereum, launchpad, permissioned, tier-system, kyc, sho]
confidence: high
last_updated: 2026-04-02
sources:
  - https://daomaker.com/
  - https://coinmarketcap.com/alexandria/article/what-is-dao-maker
---

## Summary
DAO Maker is an Ethereum-based launchpad that emphasises long-term project incubation, DAO community formation, and structured permissioned sales. Access to token sales is gated by holding/staking $DAO tokens and completing KYC. It uses a proprietary "Strong Holder Offering" (SHO) model to allocate participation based on DAO token holdings.

## Key Facts
- Total raised: $90M+ across 315,000 KYCed users and 1.1M connected wallets
- Primary sale product: Strong Holder Offering (SHO) — reserved round for $DAO stakers
- Allocation mechanism: DAO Power (derived from staked $DAO tokens) → wallet chain analysis → tier assignment
- The more $DAO staked, the higher the tier and the larger the allocation
- KYC is mandatory and platform-managed (projects don't handle KYC separately)
- No wait time between KYC and participation (unlike Polkastarter's 7-day hold)
- Other sale types: SEED sales, Dynamic Coin Offerings (DYCOs — partially refundable model)
- Projects also supported with incubation, legal, marketing and DAO formation services
- $DAO token utility: staking for SHO access; governance participation
- Platform includes Airdrops, Farms, Vaults, and Staking products beyond just launchpad

## How it relates to Logos
- DAO Maker's tier/SHO model is a reference for permissioned access via native token staking — directly applicable to any Logos-ecosystem launchpad design
- KYC-at-platform-level (not project level) reduces friction for projects; good UX model
- DYCO (refundable token offering) is an interesting primitive for risk mitigation — worth exploring for Logos

> [!fact] DAO Maker handles KYC centrally — differentiator vs. Polkastarter where each project manages their own KYC

> [!analysis] Strong Holder model creates Sybil resistance via economic stake, but concentrates power with large token holders — plutocratic tendency

## Refund & Participant Protection

> [!fact] DYCO mechanism confirmed from official DAO Maker docs and multiple Medium articles (2020–2021)

- **Refund window:** Yes — **16 months post-TGE**. 100% of the circulating supply is backed by USDC for the first 16 months after the Token Generation Event. Participants can refund any tokens during this window.
- **Minimum raise threshold (soft cap):** Not applicable to DYCO model — the refund mechanism serves as the protection instead of a soft cap.
- **Post-launch performance refund:** Yes — **this is DYCO's core innovation.** If the token value falls below the refund price level, participants can buy tokens on the secondary market and refund them for USDC at the original price, generating risk-free arbitrage profits. Refunded tokens are automatically burned, reducing circulating supply by up to 100%.
- **Cancellation rights:** Participants can refund at any time within the 16-month window regardless of reason. The refund is not conditional on proving project failure — it's an unconditional right.

### DYCO Technical Mechanics

> [!fact] Confirmed from DAO Maker official documentation and DYCO v2.0 Medium article

1. **USD-backed tokens**: All tokens sold in a DYCO are backed 1:1 by USDC held in a smart contract for 16 months post-TGE
2. **Burn-on-refund**: When a participant refunds tokens, those tokens are sent to a burn address, permanently reducing supply
3. **Mirror flips**: If token price drops below refund value, arbitrageurs can buy cheap on market → refund at higher USDC price → profit. This creates reliable buy-side pressure and price floor
4. **Static supply**: Token supply remains static during the 16-month refund period (no new minting)
5. **Team accountability**: If the project under-delivers, mass refunds burn supply and return capital to investors; the team loses both capital and circulating tokens

### DYCO v2.0 Enhancements

> [!fact] From DAO Maker Medium (Dec 2021)

- **Toll Bridge mechanism**: DYCO v2 adds flexible release schedules — participants can claim their entire allocation early but must burn a portion as a "toll" that decreases daily to 0% at final distribution
- **Secondary market confidence**: The toll bridge ensures market price isn't excessively distorted from primary buyers' target exit prices, since primary buyers can sell early (at a burn cost) rather than waiting for scheduled releases
- **Retained refund rights**: All original DYCO refund mechanics (USD backing, burn-on-refund, mirror flips) remain intact in v2

## Open Questions
- Is SHO smart contract open-source? What chain is the allocation contract deployed on?
- ~~How does DYCO's refund mechanism work technically?~~ → **Resolved:** See Refund & Participant Protection section above
- Has DAO Maker experienced hacks or exploits? (Platform had a $7M exploit in 2021 — check current security posture)
- How many projects have actually used DYCO vs SHO? Is DYCO still actively offered in 2025–2026?

## Sources
- https://app.daomaker.com/
- https://coinmarketcap.com/alexandria/article/what-is-dao-maker
- https://coinpaper.com/3005/dao-maker-revolutionizing-venture-capital-for-the-crypto-era
