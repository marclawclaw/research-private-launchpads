---
topic: Refund Mechanisms Comparison
type: analysis
tags: [refund, grace-period, participant-protection, comparison, launchpad]
confidence: high
last_updated: 2026-04-02
sources:
  - https://learn.daomaker.com/dyco
  - https://medium.com/daomaker/dyco-v2-0-the-next-stage-for-dynamic-coin-offerings-ddbab4b85aea
  - https://developers.metaplex.com/smart-contracts/genesis/launch-pool
  - https://www.metaplex.com/token/so9mVZLFvnFSmiVVC9qiJhZugBMjtHkPaHtdAKDPLEX
  - https://docs.streamflow.finance
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
  - https://www.ecfr.gov/current/title-17/chapter-II/part-227
  - https://www.sec.gov/rules-regulations/staff-guidance/trading-markets-frequently-asked-questions/cfportal-faqs
---

## Summary

Cross-protocol comparison of refund windows, grace periods, minimum raise thresholds, and participant protection mechanisms across private/permissioned launchpad and token sale platforms. Most crypto-native platforms offer **no refund mechanism** — purchases are final AMM swaps or fixed-price transactions. The notable exceptions are DAO Maker's DYCO (16-month performance-based refund), Metaplex Genesis Launch Pool (soft cap refund if goal unmet), and SEC Reg CF mandated cancellation rights (48-hour window + minimum raise threshold).

## Comparison Matrix

| Protocol | Refund Window | Minimum Raise (Soft Cap) | Post-Launch Performance Refund | Cancellation Rights |
|----------|:---:|:---:|:---:|:---:|
| **DAO Maker (DYCO)** | ✅ 16 months | ❌ | ✅ USDC-backed burn refund | ✅ Unconditional within window |
| **DAO Maker (SHO)** | ❌ | ❌ | ❌ | ❌ |
| **Fjord Foundry (LBP)** | ❌ | ❌ | ❌ | ⚠️ Sell back at market price during sale only |
| **Polkastarter (IDO)** | ❌ | ❌ | ❌ | ❌ (pre-purchase only) |
| **LBP (Balancer)** | ❌ | ❌ | ❌ | ⚠️ Sell back at market price if buy+sell mode |
| **Metaplex Genesis (Launch Pool)** | ⚠️ Pre-claim withdrawal | ✅ Goal-based refund | ❌ | ✅ Withdraw during deposit window |
| **Metaplex Genesis (Presale)** | ❌ | ❌ | ❌ | ❌ (FCFS, no refund) |
| **Streamflow** | N/A (vesting, not sale) | N/A | N/A | ⚠️ Issuer-side cancellation only |
| **Securitize (Reg D/S)** | ❌ Native | ❌ Native | ❌ | ⚠️ Per offering terms (issuer-defined) |
| **Republic (Reg CF)** | ✅ Until 48h before deadline | ✅ Mandatory target | ❌ | ✅ Cancel for any reason pre-deadline |
| **EU MiCA** | ✅ 14-day cooling-off | Depends on framework | ❌ | ✅ 14-day right of withdrawal |

## Key Facts

### Tier 1: Strong Refund Protection

> [!fact] Only two platforms offer genuine post-purchase refund mechanisms

1. **DAO Maker DYCO** — 16-month USDC-backed refund window. 100% of circulating supply backed by USDC in smart contract. Refunded tokens are burned, reducing supply. Creates price floor via arbitrage (buy cheap on market → refund at USDC price). Unique "Toll Bridge" mechanism in v2 allows early exit with proportional token burn.

2. **Republic / Reg CF** — SEC-mandated 48-hour cancellation window before offering deadline. Mandatory minimum raise threshold — if target not met, all funds returned. Material change to offering terms triggers automatic cancellation unless investor reconfirms within 5 business days.

### Tier 2: Partial / Conditional Protection

> [!fact] These platforms offer withdrawal during the sale, but no post-purchase refund

3. **Metaplex Genesis Launch Pool** — Withdrawals allowed during deposit window (2% fee). If the sale goal is not met, buyers can claim a full refund of their deposits. Once the claim period begins and tokens are distributed, purchases are final.

4. **LBP / Fjord Foundry** — In buy+sell mode, participants can sell tokens back into the pool during the sale at current AMM price (which may be lower than purchase price). No guaranteed refund. After sale ends, tokens are distributed with no refund mechanism.

### Tier 3: No Refund

> [!analysis] Most crypto-native platforms treat purchases as final

5. **Polkastarter** — Fixed-price IDO purchases are final once executed. No refund, no soft cap, no grace period.

6. **Securitize** — No native refund mechanism in the platform. Rescission rights may exist per offering documents (issuer-defined, not platform-enforced). As a securities platform, individual offerings may include contractual withdrawal rights, but this is offering-specific, not systemic.

7. **Streamflow** — Vesting/distribution infrastructure only. Contract cancellation is issuer-initiated (clawback of unvested tokens), not investor-initiated refund.

## Regulatory Context

> [!fact] Regulatory frameworks increasingly mandate refund/cooling-off protections for token sales

| Regulation | Refund Mechanism |
|------------|-----------------|
| **US Reg CF** | 48-hour cancellation + mandatory minimum raise + material change re-confirmation |
| **US Reg D** | No mandatory cooling-off (accredited investors assumed sophisticated) |
| **EU MiCA** | 14-day right of withdrawal for crypto-asset purchases from a white paper offering |
| **UK (proposed)** | 14-day cooling-off period proposed in consultation for crypto-asset sales |

> [!analysis] The EU MiCA 14-day cooling-off period is the most aggressive regulatory refund requirement. Any platform operating in the EU post-MiCA will need to implement refund mechanics. This creates a design opportunity for on-chain refund infrastructure.

## Design Implications for Logos

> [!analysis] Based on the user question: "Would there be no refund state enabled even if minimum target is reached? Usually, a participant is offered a 3-day period for refunds if performance is bad."

1. **The "3-day refund period" pattern** maps most closely to:
   - Reg CF's 48-hour pre-deadline cancellation (regulatory)
   - EU MiCA's 14-day cooling-off (regulatory)
   - DAO Maker DYCO's 16-month performance refund (voluntary, market-leading)

2. **A Logos launchpad should consider implementing:**
   - **Mandatory soft cap** with automatic refund if minimum not met (like Metaplex Genesis Launch Pool)
   - **Post-launch grace period** (e.g., 3–7 days) where participants can claim a refund at purchase price — this would be novel in crypto-native platforms and a competitive differentiator
   - **Performance-based refund window** (DYCO-inspired) where tokens remain USDC-backed for a period, enabling refunds if performance disappoints

3. **Smart contract design**: Refund mechanics require escrowing raised funds (USDC/SOL) in a contract rather than releasing directly to the project. This creates tension with project capital needs but dramatically increases investor confidence.

## How it relates to Logos

- A privacy-preserving refund mechanism (ZK-proof that you participated + refund without revealing identity) would be a unique Logos contribution
- The DAO Maker DYCO model is the gold standard for on-chain refund mechanics — worth studying for a Logos implementation
- Reg CF compliance (if applicable) mandates cancellation rights that could be enforced on-chain via smart contract
- EU MiCA 14-day cooling-off will require infrastructure support — early movers building this will have regulatory advantage

## Sources

- https://learn.daomaker.com/dyco
- https://medium.com/daomaker/dyco-v2-0-the-next-stage-for-dynamic-coin-offerings-ddbab4b85aea
- https://developers.metaplex.com/smart-contracts/genesis/launch-pool
- https://www.metaplex.com/token/so9mVZLFvnFSmiVVC9qiJhZugBMjtHkPaHtdAKDPLEX
- https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
- https://www.ecfr.gov/current/title-17/chapter-II/part-227 (Reg CF)
- https://www.sec.gov/rules-regulations/staff-guidance/trading-markets-frequently-asked-questions/cfportal-faqs
- https://www.shoosmiths.com/insights/articles/heating-up-consumer-protection-for-crypto-assets (EU MiCA cooling-off)
