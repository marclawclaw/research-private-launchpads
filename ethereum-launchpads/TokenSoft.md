---
topic: TokenSoft
type: competitor
tags: [ethereum, token-distribution, compliance, kyc, whitelist, erc-1404, sto]
confidence: high
last_updated: 2026-04-02
sources:
  - https://www.tokensoft.com/
  - https://tokensoft.gitbook.io/tokensoft/api/use-cases
  - https://tokenist.com/tokensoft-ceo-explains-security-token-whitelisting/
---

## Summary
TokenSoft is a compliance-as-a-service token distribution platform that manages KYC/KYB/AML verification and on-chain whitelisting for token sales, airdrops, and vesting distributions. It enforces that only verified investors can hold or receive tokens, using ERC-1404 compatible smart contracts with transfer restrictions. Over $1B raised by customers.

## Key Facts
- Platform-as-a-service: issuers get managed portal for investor onboarding; investors get claim/distribution UI
- Supports ERC-20 tokens on Ethereum and other EVM chains
- Compliance team handles KYC, KYB, and accredited investor checks as a managed service (not just tooling)
- Works with SAFT agreements, vesting schedules, airdrop distributions
- Batch distribution supported for large recipient sets
- API-based whitelisting: ATS partners can request on-chain whitelisting of verified investors
- Developer APIs available for custom integrations
- Long-standing platform (2017+); high-profile DeFi and crypto clients

## Allowlist & Access Control

> [!fact] Confirmed from TokenSoft API docs, Tokenist interview with CEO, and platform documentation

- **Gating method:** Mandatory KYC/KYB/AML + accredited investor verification, managed end-to-end by TokenSoft's compliance team
- **Enforcement:** Hybrid — on-chain transfer restrictions + off-chain compliance management:
  - **On-chain:** Uses ERC-1404 compatible token contracts that restrict transfers to whitelisted addresses only. Smart contracts check whitelist status before executing any transfer
  - **Off-chain:** TokenSoft's compliance team manages the entire KYC/KYB/accreditation verification process. Once an investor passes verification, their wallet address is added to the on-chain whitelist
  - **API whitelisting:** ATS (Alternative Trading System) partners can use API endpoints to request on-chain whitelisting of verified investors for secondary trading compliance
  - Transfer restrictions apply not just at sale time but continuously — tokens can only be transferred between whitelisted wallets
- **Tiered access:** Yes — regulatory tiers:
  - Accredited investors: full access to Reg D offerings
  - Non-accredited investors: limited access under applicable exemptions
  - KYB (Know Your Business): entity-level verification for institutional investors
  - Access determined by offering type and investor qualification, not by token holdings
- **Geo-blocking:** Yes — jurisdiction restrictions enforced through the compliance verification process. Investors from restricted jurisdictions are not whitelisted. Enforcement is at the compliance/onboarding layer
- **Phased rounds:** Yes — supports structured distribution phases:
  - Pre-sale/SAFT: investor-level claims with vesting schedules
  - Public distribution: airdrop and claims with configurable unlock settings
  - Post-sale: ongoing transfer restrictions ensure continuous compliance
- **Sybil resistance:** Very strong — managed compliance model:
  - Full identity verification (KYC) required for individuals
  - Business verification (KYB) required for entities
  - Accredited investor documentation required where applicable
  - On-chain whitelist means even if someone bypasses the UI, the smart contract blocks unauthorised transfers
  - One-to-one wallet-to-identity mapping enforced through the verification process

> [!analysis] TokenSoft's "compliance-as-a-service" model is distinctive — rather than just providing tools (like Fjord's whitelist CSV upload), TokenSoft's team actually performs the compliance work. This makes it the lowest-friction option for projects that want regulatory coverage without building internal compliance ops. The continuous transfer restriction (not just at sale time) via ERC-1404 is more comprehensive than platform-level gating. For Logos, TokenSoft demonstrates that compliance can be abstracted as a service layer — the question is whether ZK proofs could replace the managed compliance team while maintaining equivalent regulatory coverage.

See also: [[On-Chain KYC Providers]], [[Token Sale Permissioning Mechanisms]], [[Regulation D]]

## How it relates to Logos
- TokenSoft's ERC-1404 transfer restriction pattern could be adapted for privacy-preserving compliance using ZK proofs instead of plaintext whitelist checks
- The API-based whitelisting model is a useful reference for how external verification can feed into on-chain access control
- Compliance-as-a-service concept maps well to a potential Logos "privacy compliance oracle" — ZK attestation service that replaces manual KYC teams

## Open Questions
- Is TokenSoft's whitelist enforcement truly on-chain (Merkle proof or mapping) or does it rely on a centralised contract admin?
- Can ERC-1404 restrictions be combined with ZK proofs for privacy-preserving transfer compliance?
- What happens to whitelisted wallets if TokenSoft ceases operations — who controls the whitelist contract?

## Sources
- https://www.tokensoft.com/
- https://tokensoft.gitbook.io/tokensoft/api/use-cases
- https://tokenist.com/tokensoft-ceo-explains-security-token-whitelisting/
