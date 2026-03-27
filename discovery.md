# Discovery Report: Private Launchpads & Token Issuance

**Date:** 2026-03-27  
**Status:** Phase 1 — Discovery complete  
**Researcher:** Marclaw researcher agent

---

## Overview

The landscape of private/permissioned token issuance spans two major ecosystems (Ethereum + Solana), compliance-first infrastructure, ZK privacy layers, and cross-chain approaches. Research identified 6 core topics for deep crawls.

---

## Topics & Sources

### Topic 1: Ethereum Private/Permissioned Launchpads
Key platforms and mechanisms for permissioned token sales on Ethereum.

**Platforms:**
- Fjord Foundry (LBPs + whitelist gating) — https://www.fjordfoundry.com/
- Copper.co (LBP platform, acquired by Fjord) — https://fjordfoundry.com/
- DAO Maker — https://daomaker.com/
- Polkastarter — https://polkastarter.com/

**Sources:**
- https://www.fjordfoundry.com/
- https://balancer.gitbook.io/balancer/smart-contracts/smart-pools/liquidity-bootstrapping-faq
- https://coinlaunch.space/launchpads/round-hosting/
- https://99bitcoins.com/best-crypto-launchpads/ethereum/
- GitHub: search "ethereum private token sale launchpad"

---

### Topic 2: Solana Token Launchpads & Permissioned Sales
Solana-native launchpad programs and whitelist-gated token sale approaches.

**Platforms/Protocols:**
- solana-labs/launchpad (reference impl) — https://github.com/solana-labs/launchpad
- palsp/solana-launchpad (off-chain whitelist) — https://github.com/palsp/solana-launchpad
- Streamflow (vesting + distribution) — https://streamflow.finance/
- Underdog Protocol — whitelist NFT gating

**Sources:**
- https://github.com/solana-labs/launchpad
- https://github.com/palsp/solana-launchpad
- https://streamflow.finance/
- https://streamflow.finance/blog/token-vesting-the-definitive-guide

---

### Topic 3: Solana Token-2022 Extensions (Confidential Transfers + Permissioning)
Privacy and permissioning primitives built into Solana's Token-2022 program.

**Key extensions:**
- Confidential Transfers (ZK-encrypted amounts)
- Transfer Hooks (custom permissioning logic)
- Non-Transferable tokens
- Permanent Delegate
- Interest-Bearing tokens

**Sources:**
- https://solana.com/docs/tokens/extensions/confidential-transfer
- https://spl.solana.com/confidential-token/quickstart
- https://www.quicknode.com/guides/solana-development/spl-tokens/token-2022/confidential
- https://rareskills.io/post/token-2022
- GitHub: https://github.com/solana-labs/solana-program-library (token-2022)

---

### Topic 4: ZK Privacy-Preserving Token Issuance (Aztec + Penumbra)
Fully private token issuance using zero-knowledge proofs on privacy-first L2s/chains.

**Platforms:**
- Aztec Network (Ethereum L2, Noir language, private contracts) — https://aztec.network/
- Penumbra (Cosmos/IBC, shielded DEX + token issuance) — https://penumbra.zone/

**Sources:**
- https://aztec.network/basics
- https://aztec.network/blog/
- https://penumbra.zone/
- https://github.com/penumbra-zone/penumbra
- https://github.com/AztecProtocol/aztec-packages
- https://markaicode.com/zk-snarks-vs-zk-starks-implementation-guide/
- https://www.cache256.com/ecosystem/shielded-pools-defi-privacy-infrastructure-analysis/

---

### Topic 5: KYC-Gated / Accredited Investor Token Sales (Compliance)
Legal frameworks and on-chain KYC/AML infrastructure for compliant private token sales.

**Frameworks:**
- SAFT (Simple Agreement for Future Tokens)
- Reg D 506(b)/(c) — accredited investor exemptions
- Reg CF — crowdfunding
- On-chain KYC: Sumsub, Synaps, Parallel Markets

**Platforms with compliance layer:**
- Republic.co (Reg CF + D token sales)
- Securitize (security token issuance)
- tZero (regulated trading)

**Sources:**
- https://qubit.capital/blog/token-sales-regulations
- https://sumsub.com/blog/kyc-legal-for-sto/
- https://www.sec.gov/newsroom/speeches-statements/cf-crypto-securities-041025-offerings-registrations-securities-crypto-asset-markets
- https://www.upcounsel.com/do-you-need-to-register-your-token-offering-with-the-sec

---

### Topic 6: Token Vesting & Distribution Protocols
On-chain vesting schedules and distribution primitives (both Ethereum and Solana).

**Protocols:**
- Streamflow Finance (Solana + EVM) — https://streamflow.finance/
- Team.Finance — https://www.team.finance/vesting
- Sablier (Ethereum, streaming payments/vesting) — https://sablier.com/
- LlamaPay (streaming) — https://llamapay.io/

**Sources:**
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
- https://www.team.finance/vesting
- https://github.com/AbdelStark/token-vesting-contracts
- https://sablier.com/
- https://github.com/sablier-labs/v2-core

---

## Cron Schedule

| Topic | Label | Fires |
|-------|-------|-------|
| Topic 1: Ethereum Launchpads | `launchpad-eth` | T+0h |
| Topic 2: Solana Launchpads | `launchpad-sol` | T+3h |
| Topic 3: Token-2022 Extensions | `token2022-ext` | T+6h |
| Topic 4: ZK Privacy Issuance | `zk-privacy-issuance` | T+9h |
| Topic 5: KYC/Compliance | `kyc-compliance` | T+12h |
| Topic 6: Vesting Protocols | `vesting-protocols` | T+15h |

---

## Key Themes Identified

1. **Two distinct tracks:** (a) permissioned via whitelist/KYC at the sale level, (b) privacy-preserving via ZK at the protocol level
2. **Solana Token-2022** is the most technically sophisticated native approach — confidential transfers, transfer hooks enable private + permissioned issuance without external L2
3. **Aztec** enables fully programmable privacy (private smart contracts) but ecosystem is nascent
4. **Compliance layer** is increasingly important — on-chain KYC attestations, selective disclosure
5. **Vesting/distribution** is relatively mature (Streamflow, Sablier) but rarely combined with privacy
6. **Cross-chain gap:** no dominant cross-chain private launchpad; most solutions are chain-specific
