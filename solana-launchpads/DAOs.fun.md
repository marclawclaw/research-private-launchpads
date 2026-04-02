---
topic: DAOs.fun
type: competitor
tags: [solana, launchpad, dao, fund, memecoin, fair-launch, ragequit, refund]
confidence: high
last_updated: 2026-04-02
sources:
  - https://www.chaincatcher.com/en/article/2149146
  - https://www.chaincatcher.com/en/article/2149152
  - https://www.bitget.com/news/detail/12560604310462
  - https://blog.mevx.io/news/daos-fun-the-platform-meme-and-ai-dao-funds/
  - https://thedefiant.io/news/defi/daos-fun-launches-v3-upgrade
  - https://www.blocmates.com/news-posts/slam-crack-pow-daos-fun-is-shaking-up-the-crypto-memecoin-space
  - https://iq.wiki/wiki/daosfun
---

# DAOs.fun

## Summary
DAOs.fun is a Solana-based platform for launching investment DAO funds — primarily meme and AI-focused. Creators raise SOL over a 7-day window, then manage the pooled capital on behalf of token holders. The platform features a built-in refund mechanism: if fundraising fails, contributors can redeem their SOL (with a 10% early redemption penalty). All DAOs have a mandatory expiration (3 months to 1 year) after which profits are distributed proportionally. Backed by Alliance DAO.

## Key Facts

### Mechanism
- **Fundraising window:** 7 days to reach a preset hard cap in SOL
- **Fair launch:** All participants buy DAO tokens at the same price during the fundraising phase
- **Fund management:** Creator invests raised SOL into Solana protocols/memecoins on behalf of token holders
- **Token trading:** After successful raise, DAO tokens trade on a virtual AMM; price reflects fund performance + market sentiment
- **Expiration:** All DAOs have mandatory expiration dates (3 months to 1 year), set by the creator at launch
- **Post-expiry:** DAO wallet frozen; SOL profits distributed proportionally to creators and investors
- **Creator-set parameters:** Fundraising target, fund expiration time, management fees
- **Access:** Originally invitation-only (creator codes from @baoskee or official team); later expanded
- **V3 upgrade (Nov 2024):** Added staking to earn fees and delegated investment rights

### Refund & Participant Protection

> [!fact] Confirmed from ChainCatcher, Bitget News, Mevx blog, Blocmates

- **Refund on fundraising failure:** Yes — if the 7-day fundraising period ends without reaching the hard cap, contributors can redeem their SOL
- **Early redemption penalty:** 10% loss on early redemption (before fundraising period ends)
- **Post-raise refund:** No direct refund. Once fundraising succeeds:
  - Token holders can sell DAO tokens on the virtual AMM at market price
  - Price downside is limited to the fundraising market value (floor)
  - Token holders can burn DAO tokens to redeem underlying assets at expiry
- **Expiry distribution:** At fund expiration, all remaining assets are distributed proportionally. Token holders can:
  1. Burn tokens to redeem underlying SOL/assets
  2. Sell tokens on the open market (if market value > fundraising amount)
- **Price floor:** As long as the token's market value exceeds the original fundraising amount, holders can exit via the AMM. Below that, selling is restricted

> [!analysis] DAOs.fun has the most structured refund mechanism among Solana launchpads:
> - **Pre-raise:** Full refund minus 10% penalty (ragequit during fundraising)
> - **Post-raise:** No refund, but AMM exit + mandatory expiry distribution
> - **At expiry:** Proportional asset redemption (burn-to-redeem)
>
> The 10% early redemption penalty is a Sybil-resistance mechanism — it penalizes speculative allocation-grabbing during the raise window. The mandatory expiry + proportional distribution is similar to traditional fund structures (closed-end funds). This is fundamentally different from pump.fun (no refund, no expiry) and Fjord (no refund, LBP is final).
>
> For Logos: The ragequit + burn-to-redeem model is directly relevant to privacy-preserving fund launches. A ZK version could hide individual redemption amounts while proving total redemptions don't exceed the pool. The mandatory expiry prevents infinite fund extraction by managers.

### Allowlist & Access Control

> [!fact] Confirmed from ChainCatcher and IQ.wiki
- **Gating method:** Invitation-only for creators (invite codes from @baoskee or official team); open participation for buyers once a DAO is live
- **Enforcement:** Platform-level (invite code system for creators); no on-chain permissioning for participants
- **KYC:** None
- **Sybil resistance:** 10% early redemption penalty discourages speculative multi-wallet participation during fundraising

### Fee Structure

> [!analysis] Partially inferred — exact platform fees not fully documented

- **Creator management fee:** Set by creator at launch (variable, creator-defined)
- **Platform fee:** Not explicitly documented in sources
- **Early redemption penalty:** 10% of contributed SOL (on withdrawal before fundraising ends)
- **V3 staking fees:** Stakers earn fees from the platform (details from V3 upgrade, Nov 2024)

### Scale & Traction

> [!outdated] Limited aggregate data available. Not tracked on DefiLlama.

- **Notable DAOs:** ai16z (peaked near $100M market cap, settled ~$45M); Kotopia (raised 4,207 SOL ≈ $740K)
- **Market value to NAV ratios:** Extremely high at peak — ai16z at 58x, SEQUOAI at 40x, NORM at 29x (Oct 2024)
- **Platform status:** Active as of 2025; V3 upgrade launched Nov 2024
- **CoinGecko listing:** Tracked as an exchange (daos-fun)
- **No aggregate volume/TVL/revenue data publicly available**

## How it relates to Logos

- **Ragequit model is the strongest refund mechanism studied** — directly transferable to a Logos privacy-preserving launchpad. ZK ragequit could prove "I exited" without revealing which wallet or how much
- **Mandatory fund expiry** prevents indefinite lock-up — a trust-minimizing property. Could be enforced via timelock contracts on Logos
- **10% early redemption penalty** is an elegant economic Sybil-resistance mechanism that doesn't require KYC — worth studying for Logos fair launches
- **Market value vs NAV divergence** (58x for ai16z) highlights a risk in DAO fund models — Logos could use ZK to hide NAV composition while proving solvency
- **Creator accountability via Twitter-linked identity** — minimal but non-zero reputation staking. Logos could replace this with ZK reputation proofs

## Open Questions

- What is the exact platform fee percentage (if any)?
- How does the V3 staking mechanism work technically — is it on-chain?
- What is the total number of DAOs launched and total SOL raised across all DAOs?
- Does the virtual AMM have any privacy features or is all trading fully transparent?
- Has any DAO actually completed its full lifecycle (raise → manage → expire → distribute)?

## Sources

1. ChainCatcher — "daos.fun: The next liquidity black hole?" (Oct 2024) — Full mechanism description, refund rules
2. ChainCatcher — "Analyzing daos.fun" (Oct 2024) — 10% early redemption penalty, fundraising stages
3. Bitget News — "daos.fun: The next liquidity black hole?" (Oct 2024) — Fundraising failure refund, early redemption
4. Mevx Blog — "Daos.fun: The Platform Empowering Meme and AI DAO Funds" (Feb 2025) — Fee structure, creator setup
5. The Defiant — "DAOs.Fun Launches V3 Upgrade" (Nov 2024) — V3 staking, delegated investment rights
6. Blocmates — "Daos.fun is Shaking Up the Crypto Memecoin Space" (Jan 2025) — Fund expiry (3 months to 1 year)
7. IQ.wiki — "DAOs.Fun" (Jan 2025) — Token trading, redemption options, Kotopia raise data
