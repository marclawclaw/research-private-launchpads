---
topic: Securitize
type: competitor
tags: [ethereum, security-token, permissioned, kyc, ds-protocol, compliance, rwa]
confidence: high
last_updated: 2026-04-02
sources:
  - https://securitize.io/
  - https://github.com/securitize-io/dstoken
  - https://medium.com/securitize/introducing-ds-digital-securities-protocol-securitizes-digital-ownership-architecture-for-4bcb6a9c4a16
  - https://www.bitcoinlandlords.com/post/securitize-regulated-tokenization-infrastructure-for-real-estate-and-private-market-assets
---

## Summary
Securitize is an SEC-registered transfer agent and broker-dealer providing full-stack security token issuance infrastructure. Its DS (Digital Securities) Protocol enforces transfer restrictions at the smart contract level, ensuring only KYC/AML-verified and accredited investors can hold or transfer tokens. Used by BlackRock (BUIDL fund), Apollo, KKR, and Hamilton Lane for on-chain securities.

## Key Facts
- SEC-registered transfer agent and broker-dealer (via Securitize Markets)
- DS Protocol: layered smart contract architecture with Registry Service, Compliance Service, Trust Service
- ~$2B in on-chain tokenized securities issued
- Supports Reg D, Reg S, Reg A+, and Reg CF offerings
- DS Token is ERC-20 superset — every transfer checked against Compliance Service before execution
- DSToken v4 (latest): adds Transfer Agent role, real-time rebasing, EIP-712 investor self-whitelisting
- Launching Converge chain (with Ethena) — institutional DeFi blockchain for permissioned DeFi
- Open-source reference implementation: `securitize-io/dstoken` on GitHub

## Allowlist & Access Control

> [!fact] Confirmed from DS Protocol GitHub repo, Securitize Medium articles, and SEC submission (May 2025)

- **Gating method:** Mandatory KYC/AML + accredited investor verification. All investors must pass identity verification and regulatory qualification checks before receiving tokens
- **Enforcement:** On-chain (smart contract). DS Protocol enforces compliance at the token transfer level:
  - **Registry Service:** On-chain database of investors with hashed identity data, accreditation status, and confirmed wallet addresses. Personal data stored as hashed identifiers for privacy
  - **Compliance Service:** Smart contract that enforces transfer rules — restricts by country, limits retail investor count, requires accredited status, prevents flowback of off-shore tokens
  - Three compliance modes: (1) Full/Regulated — jurisdiction + accreditation + investor limits, (2) WhiteList — simple address-based allowlist, (3) Global Whitelist + Blacklist — combined allow/deny with BlackListManager
  - **Trust Service:** Role-based access control (Master, Issuer, Exchange, Transfer Agent roles) governing who can modify compliance rules
  - DSToken v4: **EIP-712 investor self-whitelisting** — investors can submit signed attestations to whitelist themselves, reducing issuer friction
- **Tiered access:** Yes — regulatory tiers:
  - Accredited investors: unrestricted participation in Reg D offerings
  - Non-accredited investors: limited participation under Reg CF ($5M cap, investment limits based on income/net worth)
  - Qualified purchasers / institutional investors: access to larger offerings
  - Country-specific tiers (e.g., US vs non-US rules differ per Reg D/S)
- **Geo-blocking:** Yes — enforced on-chain. Compliance Service can restrict transfers to/from specific countries. Investor country stored in Registry Service. "Preventing flowback of off-shore tokens" is a native compliance rule (blocks offshore tokens returning to restricted jurisdictions)
- **Phased rounds:** Yes — offerings typically have structured phases: private placement (Reg D accredited only) → possible Reg CF public round. Converge chain enables DeFi-layer secondary trading with continuous compliance enforcement
- **Sybil resistance:** Very strong — mandatory identity verification tied to wallet addresses via Registry Service. One identity = one set of wallets. Exchange role allows third-party ATS platforms to register verified investors. BlackListManager provides explicit deny capabilities for sanctioned/flagged wallets

> [!analysis] Securitize represents the gold standard for on-chain compliance enforcement. The DS Protocol's transfer-level gating means tokens physically cannot move to non-compliant wallets — this is fundamentally different from platform-level gating (Fjord) or staking-based access (DAO Maker). The tradeoff is zero privacy: all investor data (hashed but deterministic) is on-chain and linkable. DSToken v4's EIP-712 self-whitelisting is an interesting step toward reducing centralisation of the onboarding flow. For Logos, DS Protocol's architecture is a reference for how compliance can be encoded in smart contracts, but the privacy gap (no ZK proofs for accreditation) is the clear opportunity.

See also: [[On-Chain KYC Providers]], [[Token Sale Permissioning Mechanisms]], [[Regulation D]]

## How it relates to Logos
- DS Protocol's Compliance Service architecture is the target to replace with ZK-proof equivalents — prove accreditation without revealing identity
- Registry Service could be reimagined using Logos' Waku for off-chain identity coordination + on-chain ZK proofs for verification
- The Transfer Agent role (v4) mirrors traditional securities infrastructure — useful reference for regulated Logos token launches
- Converge chain shows the institutional demand for permissioned DeFi — Logos privacy stack could enable a privacy-preserving alternative

## Open Questions
- Can DS Protocol's Compliance Service be replaced with a ZK-proof verifier while maintaining regulatory compliance?
- How does hashed identity data in Registry Service interact with GDPR right-to-erasure?
- Is DSToken v4's self-whitelisting mechanism compatible with ZK attestations?

## Sources
- https://securitize.io/
- https://github.com/securitize-io/dstoken
- https://medium.com/securitize/introducing-ds-digital-securities-protocol-securitizes-digital-ownership-architecture-for-4bcb6a9c4a16
- https://www.bitcoinlandlords.com/post/securitize-regulated-tokenization-infrastructure-for-real-estate-and-private-market-assets
- https://x.com/Securitize/status/1978839972963631517
