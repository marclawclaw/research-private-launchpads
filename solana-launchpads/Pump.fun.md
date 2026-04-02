---
topic: Pump.fun
type: competitor
tags: [launchpad, solana, memecoin, bonding-curve, permissionless]
confidence: high
last_updated: 2026-04-02
sources: [https://www.coindesk.com/coindesk-news/2025/12/10/most-influential-pump-fun, https://tokenomics.com/articles/pumpfun-tokenomics-how-pump-distributes-45m-monthly-to-holders, https://cryptopotato.com/pump-fun-leads-as-solana-app-revenue-hits-2-4b-in-2025/, https://coinlaunch.space/projects/pumpfun/, https://www.metaplex.foundation/blog/articles/metaplex-1h-25-recap]
---

# Pump.fun

## Summary
Pump.fun is the dominant permissionless memecoin launchpad on Solana, using bonding curves for instant token creation and automated graduation to DEX liquidity. It has generated over $150B in cumulative trading volume and $818M+ in cumulative revenue, making it the largest token launchpad by volume in crypto history.

## Key Facts

> [!fact] Confirmed from multiple sources (CoinDesk, Tokenomics.com, CryptoPotato, Yahoo Finance, AInvest)
> - **Cumulative trading volume:** >$150 billion (as of Dec 2025)
> - **Cumulative protocol revenue:** >$818 million (as of early 2026)
> - **Tokens launched:** 11.7 million via Metaplex (H1 2025 alone)
> - **Pumpswap DEX TVL:** ~$140 million (after March 2025 launch)
> - **PUMP token sale:** $500 million raised (July 2025)

### Quarterly Revenue Breakdown

> [!fact] Confirmed from Yahoo Finance (Dec 2025) and AInvest (Jan 2026)

| Period | Quarterly Revenue | Notes |
|--------|------------------|-------|
| Q1 2024 | $2.45M | Launch phase |
| Q2 2024 | $47.9M | Rapid growth |
| Q3 2024 | ~$100M (est.) | Interpolated |
| Q4 2024 | $207.3M | |
| Q1 2025 | $256.2M | **All-time peak** ($137M in Jan alone) |
| Q2 2025 | Declining | Post-peak cooldown |
| Q3 2025 | Declining | |
| Q4 2025 | $70M | Stabilized at lower level |

**Annual totals (estimated):**
- **2024:** ~$358M (Q1-Q4 sum; launched Jan 2024)
- **2025:** ~$460M+ (peak year despite H2 decline)
- **Cumulative:** $818M+ through early 2026

> [!fact] Mechanism details
> - Bonding curve model: token price increases algorithmically as supply is purchased
> - Graduation threshold: once bonding curve fills, token migrates to Pumpswap DEX (previously Raydium)
> - Pumpswap launched March 2025 to capture DEX trading fees internally
> - All tokens created via [[Metaplex Genesis]] Token Metadata standard
> - 1% fee on bonding curve trades; additional fees on Pumpswap DEX trades
> - Permissionless: anyone can launch a token with no approval, KYC, or allowlist

> [!analysis] Market position
> - Single largest contributor to Solana launchpad revenue ($762M combined launchpad revenue in 2025, Pump.fun being the dominant share)
> - Launchpads collectively generated 11.6M tokens in 2025, more than double prior year — Pump.fun accounts for the vast majority
> - Vertically integrated with own DEX (Pumpswap) since March 2025

## How it relates to Logos

- **Polar opposite of privacy-preserving issuance:** Pump.fun is fully public, permissionless, no KYC, no allowlists — demonstrates massive demand for simple token creation
- **Scale benchmark:** $150B volume and $818M revenue show the market size for token launch infrastructure
- **Design lesson:** Bonding curve + graduation model is the dominant UX pattern; any Logos launchpad needs comparable simplicity for permissionless use cases
- **Privacy gap:** Zero privacy features — no shielded participation, no anonymous purchases, full on-chain transparency of every buyer. A ZK-enhanced launchpad could capture institutional/privacy-conscious demand that Pump.fun ignores
- **Anti-pattern for fair launches:** Pump.fun is plagued by snipers, sandwich attacks, and insider front-running — exactly the problems [[Batch Auctions and Commit-Reveal Token Sales]] and [[Penumbra ZSwap DEX]] aim to solve

## Open Questions

- What percentage of Pump.fun tokens survive beyond 24 hours? (Rug rate)
- How much of the $150B volume is wash trading or MEV bot activity?
- Will Pumpswap capture enough liquidity to threaten Raydium long-term?
- Has the PUMP token sale changed the platform's fee structure or governance?

## Sources

1. CoinDesk — "Most Influential: Pump.fun" (Dec 2025) — $150B volume, $138M monthly revenue, $500M token sale
2. Tokenomics.com — "Pump.fun Tokenomics" (Feb 2026) — $818M cumulative revenue, $137.12M peak month
3. CryptoPotato — "Pump.fun Leads Solana App Revenue" (Jan 2026) — $762M combined launchpad revenue, 11.6M tokens
4. CoinLaunch — "Pump.fun Overview" (Jul 2025) — Pumpswap TVL >$140M
5. Metaplex Foundation — "H1 2025 Recap" — 11.7M tokens launched on Pump.fun via Metaplex
