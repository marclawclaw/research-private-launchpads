# ZK Privacy-Preserving Token Issuance — Index

**Folder:** `zk-privacy-issuance/`  
**Last updated:** 2026-03-27  
**Crawled by:** researcher-agent (Phase 2)  
**Primary sources:** Aztec Network, Penumbra Zone, cache256 analysis

---

## Notes

| File | Type | One-line Summary |
|------|------|-----------------|
| [[Aztec Network Overview]] | competitor | Privacy-first Ethereum L2 with programmable ZK contracts; Alpha Mainnet at ~1 TPS as of early 2026 |
| [[Aztec.nr Framework]] | concept | Noir-based smart contract framework with high-level private note management; includes private token contract examples |
| [[Aztec Governance Model]] | concept | On-chain AZIP/AZUP process with sequencer signaling + tokenholder supermajority; no central team control |
| [[Penumbra Protocol Overview]] | competitor | Cosmos/IBC fully-shielded PoS network and DEX; all value private by default; $3.77M TVL |
| [[Penumbra ZSwap DEX]] | concept | Sealed-bid batch auction DEX preventing frontrunning; liquidity positions created anonymously |
| [[Penumbra Shielded Staking]] | concept | Per-validator delegation tokens as first-class shielded assets; private staking derivatives by default |
| [[Shielded Pools DeFi Infrastructure]] | summary | Sector overview: $1.5B TVL across Aztec/Railgun/Penumbra; post-Tornado Cash compliant pivot |
| [[ZK Token Issuance Patterns]] | analysis | Three design patterns for ZK private token launches; build opportunity identified — no production private launchpad exists |

---

## Key Takeaways

1. **No production private launchpad exists** on either Aztec or Penumbra — open build opportunity
2. **Aztec** is the right architecture for a programmable, compliance-compatible private launchpad (Ethereum-native, arbitrary contract logic)
3. **Penumbra's ZSwap sealed-bid auction** is the best existing anti-frontrun token distribution mechanism — viable today for IBC tokens
4. **Selective disclosure** is now table-stakes for any compliant shielded protocol
5. **Aztec is early-Alpha** (1 TPS, ~$8.74M TVL); Penumbra is further along on Cosmos (~$3.77M TVL, mainnet)
6. **Logos relevance:** Private token issuance with ZK-gated eligibility and selective compliance disclosure is a clear Logos use case

---

## Related Topics
- [[ethereum-launchpads/index]] — permissioned token sales on Ethereum (traditional)
- [[token2022-ext/index]] — Solana's confidential transfers (alternative ZK approach)
