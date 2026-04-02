---
topic: Allowlist Mechanisms Comparison
type: analysis
tags: [allowlist, whitelist, access-control, permissioned, comparison, kyc, sybil-resistance]
confidence: high
last_updated: 2026-04-02
sources:
  - Internal research notes
---

## Summary
Cross-protocol comparison of allowlist and access control mechanisms across 8 launchpad platforms/protocols. Platforms range from fully open (LBP) to fully regulated (Securitize, Republic), with most occupying a hybrid middle ground. The key design tensions are: privacy vs compliance, decentralisation vs Sybil resistance, and open access vs investor protection.

## Comparison Matrix

| Protocol | Gating Method | Enforcement | Tiered Access | Geo-blocking | Phased Rounds | Sybil Resistance | Privacy |
|----------|--------------|-------------|---------------|--------------|---------------|-------------------|---------|
| **[[DAO Maker]]** | Staking + KYC | Hybrid (on-chain stake, off-chain KYC) | Yes — 7 tiers (250–100k DAO) | Yes (platform) | Yes (priority → FCFS) | Strong (KYC + stake) | Low |
| **[[Fjord Foundry]]** | Optional whitelist (CSV) | Off-chain (platform) | Yes (project-defined tiers) | Yes (platform) | Yes (Seed/Private/Public) | Weak–Medium | High |
| **[[Polkastarter]]** | Staking + lottery + KYC | Hybrid (on-chain stake, off-chain lottery + KYC) | Yes — 5 tiers (1k–50k POLS) | Per-project | Yes (whitelist → FCFS) | Medium-strong | Medium |
| **[[Liquidity Bootstrapping Pool (LBP)\|LBP (general)]]** | None (open) | N/A (permissionless AMM) | No | No (protocol level) | Single phase | None | High |
| **[[Securitize]]** | KYC/AML + accreditation | On-chain (DS Protocol) | Yes (regulatory tiers) | Yes (on-chain) | Yes (Reg D → CF) | Very strong | Very low |
| **[[Republic]]** | KYC + regulatory qualification | Off-chain (platform) | Yes (regulatory tiers) | Yes (platform) | Yes (community → accredited) | Very strong | Very low |
| **[[TokenSoft]]** | KYC/KYB + accreditation | Hybrid (on-chain ERC-1404 + off-chain compliance) | Yes (regulatory tiers) | Yes (compliance) | Yes (pre-sale → distribution) | Very strong | Very low |
| **[[Metaplex Genesis]]** | Allowlist/denylist + optional KYC | On-chain (smart contract) | Partial (per-launch config) | Yes (on-chain) | Yes (buckets) | Medium–strong | Medium |

## Key Dimensions Analysed

### 1. Gating Method Spectrum

```
Open ←――――――――――――――――――――――――――――――→ Restricted
LBP  →  Fjord  →  Polkastarter  →  DAO Maker  →  Metaplex  →  TokenSoft  →  Securitize/Republic
(none)  (optional) (stake+lottery)  (stake+KYC)   (allowlist+KYC) (managed KYC)  (regulated KYC)
```

> [!analysis] The spectrum reveals two distinct paradigms: crypto-native access (token staking, lottery) vs regulatory access (KYC, accreditation). No platform successfully bridges both — the opportunity for ZK-proof-based permissioning is to combine the decentralisation of crypto-native gating with the compliance of regulated access.

### 2. On-chain vs Off-chain Enforcement

| Enforcement Level | Platforms | Tradeoff |
|-------------------|-----------|----------|
| **Fully on-chain** | Securitize (DS Protocol), Metaplex Genesis | Transparent, auditable, censorship-resistant; but no privacy |
| **Hybrid** | DAO Maker, Polkastarter, TokenSoft | Staking on-chain + KYC off-chain; practical but trust-split |
| **Fully off-chain** | Republic, Fjord | Platform controls access; simple but centralised |

> [!fact] Only Securitize and Metaplex Genesis enforce access control at the smart contract level for every transfer/deposit. All other platforms rely on platform-level gating that could theoretically be bypassed by direct contract interaction.

### 3. Sybil Resistance Mechanisms

| Mechanism | Used By | Effectiveness | Privacy Impact |
|-----------|---------|---------------|----------------|
| **Mandatory KYC** | DAO Maker, Securitize, Republic, TokenSoft | Very high | Destroys privacy |
| **Token staking (time-locked)** | DAO Maker, Polkastarter | Medium-high | Privacy-preserving |
| **Lottery + economic cost** | Polkastarter | Medium | Privacy-preserving |
| **Wallet allowlist** | Fjord, Metaplex Genesis | Low-medium (depends on curation) | Neutral |
| **None (open)** | LBP | None | Privacy-preserving |

> [!analysis] The Sybil resistance / privacy tradeoff is stark: the most Sybil-resistant mechanisms (KYC) destroy privacy, while privacy-preserving mechanisms (staking, lottery) are only partially Sybil-resistant. ZK-proof KYC is the theoretical resolution but is not deployed on any platform studied.

### 4. Tiered Access Models

**Crypto-native tiers (token-based):**
- DAO Maker: 7 tiers, 250–100k DAO staked, non-linear power bonuses
- Polkastarter: 5 tiers, 1k–50k POLS, booster multipliers on lottery tickets

**Regulatory tiers (qualification-based):**
- Securitize/Republic/TokenSoft: Accredited vs non-accredited vs institutional
- Tiers determined by legal status, not token holdings

**Project-defined tiers:**
- Fjord: Seed/Private/Public rounds with per-tier allocation caps
- Metaplex: Per-launch bucket configuration

> [!analysis] Token-based tiers are plutocratic (more money = more access) but permissionless. Regulatory tiers are meritocratic (qualification = access) but require trusted intermediaries. A Logos design could combine both: ZK-proof of qualification + token stake for ordering.

### 5. Geo-blocking Enforcement

| Level | Platforms | Bypass Difficulty |
|-------|-----------|-------------------|
| **Smart contract** | Securitize, Metaplex Genesis | Very hard (would need to spoof on-chain identity) |
| **Platform UI** | Fjord, Republic, DAO Maker | Easy (VPN, direct contract interaction) |
| **Per-project** | Polkastarter | Variable |
| **None** | LBP | N/A |

> [!fact] Only Securitize and Metaplex Genesis enforce geo-blocking at the smart contract level. For all other platforms, a technically sophisticated user could bypass geo-restrictions by interacting directly with the underlying contracts.

## Logos Opportunity Assessment

> [!analysis] Gap analysis for privacy-preserving access control

The research reveals four clear gaps that Logos infrastructure could fill:

1. **ZK-proof KYC/accreditation:** No platform offers privacy-preserving investor qualification. Prove "I am accredited" or "I am not in a restricted country" without revealing identity. Target: replace Securitize/Republic's identity-destroying compliance with ZK equivalents.

2. **Decentralised allowlist coordination:** Current allowlists are managed by centralised platforms (Fjord CSV upload, DAO Maker central KYC). Waku could enable decentralised credential exchange; Codex could store encrypted KYC attestations.

3. **Private fair price discovery:** LBPs provide fair pricing but are fully transparent. A shielded LBP (encrypted bid amounts, ZK-proof weight calculations) would enable private price discovery for compliant token sales.

4. **On-chain compliance with privacy:** Securitize's DS Protocol and Metaplex Genesis show that on-chain compliance enforcement works. The next step is on-chain compliance enforcement with ZK privacy — transfer restrictions verified via ZK proofs rather than plaintext registry lookups.

## Open Questions
- Which ZK identity protocols (Semaphore, Worldcoin, Polygon ID) are closest to production-ready for launchpad integration?
- Can a "permissioned LBP" (Merkle-gated pool interaction + ZK KYC) achieve both fair pricing and regulatory compliance?
- How do gas costs for ZK proof verification compare to simple whitelist mapping lookups on Ethereum vs Solana?

## Sources
- Internal research notes from [[DAO Maker]], [[Fjord Foundry]], [[Polkastarter]], [[Liquidity Bootstrapping Pool (LBP)]], [[Securitize]], [[Republic]], [[TokenSoft]], [[Metaplex Genesis]]
- [[Token Sale Permissioning Mechanisms]]
- [[Off-Chain Whitelist Pattern (Merkle Proof)]]
