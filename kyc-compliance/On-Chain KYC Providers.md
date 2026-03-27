---
topic: On-Chain KYC Providers
type: concept
tags: [kyc, aml, compliance, identity, on-chain, infrastructure]
confidence: high
last_updated: 2026-03-27
sources:
  - https://sumsub.com/blog/kyc-legal-for-sto/
  - https://www.chainalysis.com/blog/introduction-to-erc-3643-ethereum-rwa-token-standard/
  - https://www.erc3643.org/news/erc-3643-presented-to-the-sec-crypto-task-force
  - https://build.avax.network/integrations/securitize
---

## Summary
On-chain KYC providers link off-chain identity verification to blockchain wallet addresses, enabling smart contracts to enforce compliance rules (accredited investor status, jurisdiction restrictions, AML screening) directly at the token transfer level. The dominant standard for this is ERC-3643; key providers include Sumsub, Synaps, Parallel Markets, and Securitize.

## Key Facts

### ERC-3643 (T-REX Standard)
- Ethereum token standard that embeds identity registry + compliance module into the token itself
- Transfers only execute if both sender and receiver are in the **Identity Registry** and pass compliance checks
- Identity Registry links wallet addresses to on-chain identity contracts ("claims")
- Claims are issued by registered **Claim Issuers** (KYC providers, accreditation verifiers)
- Compliance logic remains fully on-chain, auditable, and independent of the issuer platform
- ERC-3643 was presented to SEC Crypto Task Force in 2025 as a model for compliant tokenized securities

### Sumsub
- Full-stack identity verification: document checks, liveness, AML screening, accredited investor verification
- Used by 4,000+ clients; specifically designed for regulated crypto (STOs, exchanges)
- Provides API-based KYC that can feed into on-chain identity registries
- FATF-compliant; supports EU MiCA, US Reg D/CF, Singapore MAS frameworks

### Securitize
- End-to-end security token issuance platform: KYC/AML, investor onboarding, cap table management, ATS trading
- Uses on-chain whitelisting: only wallets that have passed KYC/AML can receive transfers
- Works with BlackRock (BUIDL fund), BNY, and major tokenized RWA issuers
- Submitted to SEC Crypto Task Force (May 2025) proposing on-chain compliance as regulatory-grade approach
- Integrated with Avalanche, Ethereum, and other EVM chains

### Republic.co
- Registered funding portal (FINRA member) for Reg CF and Reg D raises
- Token DPA product: rights to future tokens sold to non-accredited investors under Reg CF
- Mirror Tokens product (2025): tokenized exposure to private company shares (launched under Reg D)
- Handles KYC/AML, investor qualification, and ongoing reporting obligations
- Investor base: mix of retail (Reg CF) and accredited (Reg D)

### Other Providers
- **Synaps** — KYC/AML focused on DeFi and crypto projects; webhook-based integration
- **Parallel Markets** — Accredited investor verification specialist; works with equity and token platforms
- **Veriff / Onfido** — Speed-focused identity verification; less compliance-depth than Sumsub
- **Persona / Alloy** — KYC+AML for fintech; increasingly used in token issuance

> [!fact] Confirmed — Securitize SEC submission (May 2025)
> Securitize's system automatically controls transfer of tokenized securities among whitelisted investor wallets that have passed KYC and AML checks.

> [!analysis] The trend is toward on-chain enforcement of compliance (ERC-3643, transfer hooks) rather than off-chain gating only. This makes compliance auditable and removes issuer as single point of failure.

## How it relates to Logos
- Logos' privacy stack is a natural fit for privacy-preserving on-chain KYC: prove investor qualification (jurisdiction, accreditation) via ZK without revealing raw identity data
- ERC-3643's claim-issuer model could be extended with ZK proofs (prove you hold a valid KYC claim without revealing which KYC provider or personal data)
- Codex/Waku could enable confidential investor registries — key data encrypted, only transfer hooks can query compliance status
- Direct opportunity: build a ZK-KYC claim issuer compatible with ERC-3643 using Logos privacy infrastructure

## Open Questions
- Can a ZK proof of accredited status satisfy SEC's "reasonable steps" requirement under Rule 506(c)?
- Does on-chain KYC create GDPR/data protection issues if wallet-to-identity links are pseudonymous but traceable?
- Is there a privacy-preserving alternative to ERC-3643's identity registry that avoids linking wallet to real-world identity on a public chain?
- How do Sumsub and Securitize handle right-to-erasure (GDPR Article 17) for on-chain identity claims?

## Sources
- https://sumsub.com/blog/kyc-legal-for-sto/
- https://www.chainalysis.com/blog/introduction-to-erc-3643-ethereum-rwa-token-standard/
- https://www.erc3643.org/news/erc-3643-presented-to-the-sec-crypto-task-force
- https://docs.erc3643.org/erc-3643
- https://build.avax.network/integrations/securitize
- https://www.bny.com/corporate/global/en/about-us/newsroom/company-news/securitize-launches-tokenized-aaa-clo-fund-with-services-provided-by-bny-bringing-institutional-structured-credit-on-chain.html
