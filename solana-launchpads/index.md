# Solana Token Launchpads & Permissioned Sales — Index

**Phase 2 Deep Crawl completed:** 2026-03-27  
**Sources crawled:** solana-labs/launchpad, palsp/solana-launchpad, streamflow.finance, Solana Compass, CryptoNews

---

## Notes

| File | Type | One-line summary |
|------|------|-----------------|
| [Solana Launchpad Reference Implementation](./Solana%20Launchpad%20Reference%20Implementation.md) | concept | Official SPL reference for trustless token sales with dynamic pricing; no native permissioning |
| [Off-Chain Whitelist Pattern (Merkle Proof)](./Off-Chain%20Whitelist%20Pattern%20(Merkle%20Proof).md) | concept | Dominant permissioned-sale pattern: Merkle root on-chain, buyer submits proof at purchase |
| [Streamflow Finance - Token Distribution Platform](./Streamflow%20Finance%20-%20Token%20Distribution%20Platform.md) | competitor | $1.4B TVL Solana vesting/distribution infra; 28.5K projects; white-label portals; SDK |
| [Token Vesting Schedules](./Token%20Vesting%20Schedules.md) | concept | Types (linear/cliff/milestone/randomized), stakeholder groups, on-chain vs off-chain comparison |
| [Solana Launchpad Ecosystem Overview](./Solana%20Launchpad%20Ecosystem%20Overview.md) | summary | Ecosystem map: Pump.fun (permissionless) vs Magic Eden/DAOs.fun/Solster (structured IDOs) |
| [Metaplex Genesis](./Metaplex%20Genesis.md) | competitor | Most complete Solana-native TGE platform with on-chain KYC gating, allowlists/denylists, and geo-blocking |

---

## Key Takeaways

1. **No dominant private/KYC-gated launchpad on Solana** — gap exists for institutional-grade permissioned sales
2. **Merkle proof whitelist** is the standard on-chain permissioning primitive (cheap, scalable, off-chain list trust)
3. **Streamflow** is the go-to for vesting/distribution post-sale — mature, audited, widely adopted
4. **Solana ecosystem has bifurcated:** permissionless memecoins (Pump.fun) vs structured IDOs — no hybrid with privacy
5. Token-2022 confidential transfers + transfer hooks (covered in separate topic) would enable truly private permissioned sales
6. **Metaplex Genesis has the lowest fees** of any full-featured launchpad: 2% on deposits, zero setup costs, near-zero Solana gas. See [[../ethereum-launchpads/Fee Structure Comparison]]
7. **Metaplex Genesis is the most immutable launchpad studied** — no documented pause, no admin override, parameters locked at creation. This is the most trustless model but sacrifices all emergency intervention capability. See [[../ethereum-launchpads/Sale Lifecycle Comparison]]
7. **Metaplex Genesis has the most trustless close mechanics** — deposit windows are immutable on-chain; no documented pause/halt. No admin override. Compare with Ethereum launchpads in [[../ethereum-launchpads/Sale Lifecycle Comparison]]

## Related Topics
- [[Solana Token-2022 Extensions]] (Topic 3) — confidential transfers, transfer hooks for deeper permissioning
- [[Token Vesting & Distribution Protocols]] (Topic 6) — cross-chain vesting comparison
- [[KYC-Gated Token Sales]] (Topic 5) — compliance layer for accredited investor sales
