# Ethereum Private/Permissioned Launchpads — Index

**Phase 2 crawl completed:** 2026-03-27  
**Sources crawled:** Fjord Foundry, Balancer LBP docs, DAO Maker, Polkastarter, web search supplemental  
**Notes:** 6 atomic notes

---

## Notes

| File | Type | Summary |
|------|------|---------|
| [Fjord Foundry](./Fjord%20Foundry.md) | competitor | LBP-focused platform with optional whitelisting; no token-gating; $15M LBP raise in 2024 |
| [Liquidity Bootstrapping Pool (LBP)](./Liquidity%20Bootstrapping%20Pool%20(LBP).md) | concept | Dynamic AMM pricing mechanism; weights shift over time to enable fair price discovery and deter bots |
| [DAO Maker](./DAO%20Maker.md) | competitor | Tier-based launchpad with centralised KYC and SHO model; $90M+ raised; incubation-focused |
| [Polkastarter](./Polkastarter.md) | competitor | POLS-staking lottery-based IDO access; 7-day hold requirement; per-project KYC |
| [Token Sale Permissioning Mechanisms](./Token%20Sale%20Permissioning%20Mechanisms.md) | concept | Comparative overview of allowlist, stake-gate, KYC, and ZK-proof mechanisms |
| [Strong Holder Offering (SHO)](./Strong%20Holder%20Offering%20(SHO).md) | concept | DAO Maker's proprietary staking-based guaranteed allocation model |
| [Refund Mechanisms Comparison](./Refund%20Mechanisms%20Comparison.md) | analysis | Cross-protocol comparison of refund windows, grace periods, soft caps, and participant protection |

---

## Key Insights

1. **Two paradigms**: Open LBP (Fjord) vs. staked-access IDO (DAO Maker, Polkastarter)
2. **Permissioning is always a layer on top** — no platform natively does ZK-proof gating yet
3. **KYC centralisation is the main tension** — DAO Maker centralises it (UX win), Polkastarter delegates it (decentralisation win)
4. **Opportunity gap**: Privacy-preserving permissioned launchpad (ZK-proof KYC + Logos stack) doesn't exist yet
5. **LBP bot deterrence** is elegant but doesn't prevent Sybil attacks at the participation level
6. **Refund mechanisms are rare in crypto-native platforms** — only DAO Maker DYCO offers genuine post-purchase performance-based refunds; Reg CF mandates cancellation rights; most platforms treat purchases as final (see [[Refund Mechanisms Comparison]])

---

## Related Topics
- [[Solana Token Launchpads]] (Topic 2)
- [[ZK Privacy for Token Sales]] (if covered in other topics)
