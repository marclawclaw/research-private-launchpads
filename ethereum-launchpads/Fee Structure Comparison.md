---
topic: Fee Structure Comparison
type: analysis
tags: [fees, comparison, launchpad, vesting, pricing, revenue-model]
confidence: high
last_updated: 2026-04-02
sources:
  - https://dao-maker-1.gitbook.io/dao-maker
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
  - https://docs.streamflow.finance/en/articles/9675153-costs-of-using-streamflow
  - https://docs.sablier.com/concepts/protocol/fees
  - https://hedgey.finance/
  - https://developers.metaplex.com/smart-contracts/genesis
  - https://republic.com/learn/issuers/costs
  - https://securitize.io/fee-schedule
  - https://docs.balancer.fi/concepts/governance/protocol-fees.html
---

## Summary
Cross-platform comparison of fee structures across launchpads, token sale platforms, and vesting protocols studied in this research. Covers issuer fees, participant fees, staking requirements, and revenue models. Platforms range from completely free (Hedgey, Sablier) to enterprise-priced (Securitize, TokenSoft).

## Fee Comparison Matrix

### Launchpad / Token Sale Platforms

| Platform | Issuer Fee | Buyer Fee | Setup Cost | Staking Required | Chain |
|----------|-----------|-----------|------------|-----------------|-------|
| **[[Metaplex Genesis]]** | 0% (fee on deposits) | 2% on deposits | Free | None | Solana |
| **[[Fjord Foundry]]** | 5% of collateral | Swap fee only (1-2%) | Free | None ($FJO not required) | Multi-chain |
| **[[DAO Maker]]** | 5% of tokens | 5% (DAO SHO) / 30% (Public SHO) | Undisclosed | 2,000-100,000 DAO ($28-$1,400+) | Ethereum |
| **[[Polkastarter]]** | ~1% of raised | Network gas only | Undisclosed | 1,000-50,000 POLS ($300-$25,000) | Multi-chain |
| **[[Republic]]** | 6% cash + 2% securities | None | $0-$3,500 legal | None (regulatory) | Off-chain |
| **[[Securitize]]** | Custom enterprise | 1% ATS trade commission | $50k-$500k+ (est.) | None (regulatory) | Ethereum |
| **[[TokenSoft]]** | Custom enterprise | None | $25k-$200k+ (est.) | None (regulatory) | EVM |
| **[[Liquidity Bootstrapping Pool (LBP)\|Balancer LBP]]** | 50% of swap fees (protocol) | Swap fee (0.01-10%) | Gas only ($50-200) | None | Ethereum/L2 |

### Vesting / Distribution Protocols

| Platform | Protocol Fee | Per-Contract Cost | Recipient Fee | Native Token Required | Chain |
|----------|-------------|-------------------|---------------|----------------------|-------|
| **[[Hedgey Finance]]** | Free (0%) | Gas only | Free | No | EVM + Solana |
| **[[Sablier Protocol]]** | Free (0%) | Gas only | Free | No (no token) | 27 EVM + Solana |
| **[[Streamflow Finance]]** | 0.16 SOL/contract (~$20) | 0.16 SOL + gas | 0.009-0.017 SOL/claim | No (STREAM optional) | Solana |

## Key Facts

> [!fact] Data verified from official documentation for each platform as of April 2026

### Cheapest to Most Expensive (Issuer Perspective)

1. **Hedgey / Sablier** — Free (vesting only, no token sale features)
2. **Metaplex Genesis** — 0% issuer fee (2% borne by depositors); free setup
3. **Streamflow** — ~$20/contract flat fee; Solana gas negligible
4. **Balancer LBP (direct)** — Gas costs only ($50-200 pool creation); protocol takes 50% of swap fees
5. **Fjord Foundry** — 5% of collateral raised; no upfront cost
6. **Polkastarter** — ~1% of raised; undisclosed setup/partnership costs
7. **DAO Maker** — 5% of tokens + incubation commitments
8. **Republic** — 6% cash + 2% securities (~8% effective total)
9. **TokenSoft** — Custom enterprise ($25k-200k+ estimated)
10. **Securitize** — Custom enterprise ($50k-500k+ estimated + ongoing fees)

### Cheapest to Most Expensive (Participant Perspective)

1. **Republic / TokenSoft** — Zero participant fees (issuer bears all costs)
2. **Sablier / Hedgey** — Gas only (no protocol fees)
3. **Polkastarter** — Gas only (but $300-25k staking requirement for access)
4. **Streamflow** — 0.009-0.017 SOL per airdrop claim (~$1-2)
5. **Metaplex Genesis** — 2% on deposits
6. **Fjord Foundry** — Swap fees (1-2% typical)
7. **Balancer LBP** — Swap fees (configurable, 0.01-10%)
8. **Securitize** — 1% on secondary trades
9. **DAO Maker (DAO SHO)** — 5% of tokens
10. **DAO Maker (Public SHO)** — 30% of tokens (unless buying 2,000 DAO)

## How it relates to Logos

> [!analysis] Fee structure analysis for Logos ecosystem launchpad design

### Strategic Implications

1. **Free/cheap wins adoption:** Sablier, Hedgey, and Metaplex Genesis demonstrate that zero/low fees drive adoption. Any Logos vesting or launch infrastructure should aim for minimal fees to compete
2. **Fee placement matters:** Metaplex charges depositors (not issuers); Fjord charges issuers (not buyers). The choice of who pays affects adoption dynamics — charging issuers is friendlier for community growth
3. **Staking-as-implicit-fee:** DAO Maker and Polkastarter's staking requirements function as hidden fees (capital lockup cost). This is a powerful revenue model (token demand) but creates plutocratic access barriers
4. **Enterprise vs DeFi pricing:** Securitize/TokenSoft operate in a completely different pricing tier ($50k-500k+) serving institutional regulated markets. Logos could position between these extremes — privacy-preserving compliance at DeFi pricing
5. **Revenue sustainability:** Sablier and Hedgey are free but depend on VC funding. Metaplex Genesis's 2% protocol fee is small but sustainable. The 2-5% range appears to be the sweet spot for sustainable protocol-level fees

### Recommended Fee Model for Logos Launchpad
- **Protocol fee:** 1-2% on deposits/raises (competitive with Metaplex Genesis, below Fjord)
- **Participant fee:** 0% or gas-only (competitive with Republic/Sablier)
- **Setup cost:** Free or minimal (no enterprise pricing barrier)
- **No token-gating:** Follow Fjord/Metaplex model of not requiring a native token to participate
- **Privacy premium:** Privacy features (ZK-proof KYC, shielded allocations) could justify a small premium over non-private alternatives

## Open Questions
- How do fee structures change during bear vs bull markets? Do platforms reduce fees to maintain volume?
- Are there volume-based fee discounts for large raises on any of these platforms?
- How do gas costs on various L2s compare for full token launch lifecycles?

## Sources
- Individual protocol notes in this repository (see wikilinks above)
- Official documentation and help centers for each platform
- Third-party reviews from CryptoRank, Business.org, DefiLlama, and industry analysis
