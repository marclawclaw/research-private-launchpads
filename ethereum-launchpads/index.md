# Ethereum Private/Permissioned Launchpads — Index

**Phase 2 crawl completed:** 2026-03-27  
**Gap analysis update:** 2026-04-02 (RFP-015/016 PR review)  
**Sources crawled:** Fjord Foundry, Balancer LBP docs, DAO Maker, Polkastarter, web search supplemental, Flaunch, Gnosis Auction, Uniswap V4 docs  
**Notes:** 10 atomic notes (4 added 2026-04-02)

---

## Notes

| File | Type | Summary |
|------|------|---------|
| [Fjord Foundry](./Fjord%20Foundry.md) | competitor | LBP-focused platform with optional whitelisting; no token-gating; $15M LBP raise in 2024 |
| [Liquidity Bootstrapping Pool (LBP)](./Liquidity%20Bootstrapping%20Pool%20(LBP).md) | concept | Dynamic AMM pricing mechanism; weights shift over time; includes weight formula, spot price formula, timestamp dependency, and collateral ownership analysis |
| [DAO Maker](./DAO%20Maker.md) | competitor | Tier-based launchpad with centralised KYC and SHO model; $90M+ raised; incubation-focused |
| [Polkastarter](./Polkastarter.md) | competitor | POLS-staking lottery-based IDO access; 7-day hold requirement; per-project KYC |
| [Token Sale Permissioning Mechanisms](./Token%20Sale%20Permissioning%20Mechanisms.md) | concept | Comparative overview of allowlist, stake-gate, KYC, and ZK-proof mechanisms |
| [Strong Holder Offering (SHO)](./Strong%20Holder%20Offering%20(SHO).md) | concept | DAO Maker's proprietary staking-based guaranteed allocation model |
| [Refund Mechanisms Comparison](./Refund%20Mechanisms%20Comparison.md) | analysis | Cross-protocol comparison of refund windows, grace periods, soft caps, and participant protection |
| [Securitize](./Securitize.md) | competitor | SEC-registered transfer agent; DS Protocol enforces compliance at token transfer level; $2B+ in tokenized securities |
| [Republic](./Republic.md) | competitor | FINRA-registered funding portal; Reg CF/D/A+ token raises; broadest regulatory coverage + retail access |
| [TokenSoft](./TokenSoft.md) | competitor | Compliance-as-a-service token distribution; managed KYC/KYB; ERC-1404 on-chain transfer restrictions |
| [Allowlist Mechanisms Comparison](./Allowlist%20Mechanisms%20Comparison.md) | analysis | Cross-protocol comparison of allowlist gating, enforcement, tiers, geo-blocking, and Sybil resistance |
| [Fee Structure Comparison](./Fee%20Structure%20Comparison.md) | analysis | Cross-platform fee comparison matrix covering all launchpads, sale platforms, and vesting protocols |
| [Sale Lifecycle Comparison](./Sale%20Lifecycle%20Comparison.md) | analysis | Cross-protocol matrix of sale close mechanics, emergency halt/pause, admin override, post-close distribution, and enforcement layer |
| [Flaunch (Uniswap V4 Hooks Launchpad)](./Flaunch%20(Uniswap%20V4%20Hooks%20Launchpad).md) | competitor | Production hook-based launchpad on Base; bonding curve inside V4 pool; atomic graduation; perpetual fee routing to creators; Progressive Bid Wall |
| [Bonding Curve Rounding and Integer Arithmetic](./Bonding%20Curve%20Rounding%20and%20Integer%20Arithmetic.md) | concept | How AMMs handle rounding in integer arithmetic; V2/V3/V4 rounding direction; pool solvency invariants; graduation threshold implications |
| [Collateral Vesting for Buyer Protection](./Collateral%20Vesting%20for%20Buyer%20Protection.md) | concept | Pattern of locking raised funds in vesting/timelock contract; milestone authority design; prevents rug pulls on capital; cross-program composability |
| [Batch Auctions and Commit-Reveal Token Sales](./Batch%20Auctions%20and%20Commit-Reveal%20Token%20Sales.md) | concept | Alternative mechanisms to bonding curves; Gnosis Auction, CowSwap, Penumbra sealed-bid; stronger front-running protection; production deployments |

---

## Key Insights

1. **Two paradigms**: Open LBP (Fjord) vs. staked-access IDO (DAO Maker, Polkastarter)
2. **Permissioning is always a layer on top** — no platform natively does ZK-proof gating yet
3. **KYC centralisation is the main tension** — DAO Maker centralises it (UX win), Polkastarter delegates it (decentralisation win)
4. **Opportunity gap**: Privacy-preserving permissioned launchpad (ZK-proof KYC + Logos stack) doesn't exist yet
5. **LBP bot deterrence** is elegant but doesn't prevent Sybil attacks at the participation level
6. **Refund mechanisms are rare in crypto-native platforms** — only DAO Maker DYCO offers genuine post-purchase performance-based refunds; Reg CF mandates cancellation rights; most platforms treat purchases as final (see [[Refund Mechanisms Comparison]])
7. **Access control ranges from fully open to fully regulated** — LBPs are permissionless; Securitize enforces compliance at every transfer; the privacy-preserving middle ground (ZK-proof gating) doesn't exist yet (see [[Allowlist Mechanisms Comparison]])
8. **On-chain enforcement is rare** — only Securitize (DS Protocol) and Metaplex Genesis enforce access control at the smart contract level; most platforms rely on UI-level gating
9. **Fee structures vary wildly** — from free (Hedgey, Sablier) to 2% (Metaplex Genesis) to 5% (Fjord, DAO Maker) to enterprise pricing ($50k-500k+ for Securitize/TokenSoft). DAO Maker's 30% Public SHO fee is the highest participant fee. See [[Fee Structure Comparison]]
10. **Sale lifecycle control ranges from fully centralized to fully immutable** — DAO Maker/Republic control entire lifecycle off-chain; Sablier/Metaplex Genesis have no admin override once deployed. Only Securitize/TokenSoft offer both pause AND resume across the full token lifecycle. See [[Sale Lifecycle Comparison]]
11. **Close/halt mechanics vary by design philosophy** — fully trustless (Metaplex Genesis, Sablier) vs. centralized control (Securitize, Republic). Pause-and-resume (circuit breaker) is rare: only Fjord LBP, Balancer LBP, and Sablier Flow streams support it. See [[Sale Lifecycle Comparison]]
12. **Hook-based bonding curves are production-validated** — Flaunch on Base proves V4 hooks can implement a complete bonding curve + fair launch + atomic graduation in a single pool. No separate migration transaction. See [[Flaunch (Uniswap V4 Hooks Launchpad)]].
13. **Rounding direction matters for solvency** — every bonding curve/AMM must round tokens_out down and tokens_in up. This must be explicitly implemented in V4 hook custom curves. See [[Bonding Curve Rounding and Integer Arithmetic]].
14. **LBP collateral ownership is a trust gap** — at LBP close, all collateral was paid by buyers. Returning it to the creator in a failed/underperforming sale is returning buyer funds to the team. No current LBP implementation addresses this. See [[Liquidity Bootstrapping Pool (LBP)]].
15. **Batch auctions are the strongest anti-frontrunning alternative** — Gnosis Auction (transparent) and Penumbra ZSwap (private) provide uniform clearing price + front-running resistance that bonding curves cannot match. See [[Batch Auctions and Commit-Reveal Token Sales]].
16. **Collateral vesting for buyers is an unexplored design space** — virtually no launchpad implements milestone-gated collateral release. The milestone authority design (must exclude creator) is the key challenge. See [[Collateral Vesting for Buyer Protection]].

---

## Related Topics
- [[Solana Token Launchpads]] (Topic 2)
- [[ZK Privacy for Token Sales]] (if covered in other topics)
