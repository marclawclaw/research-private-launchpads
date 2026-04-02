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

## Fee Structure

> [!analysis] TokenSoft uses custom enterprise pricing — no public fee schedule. Inferred from platform positioning and industry norms

- **Platform fee (issuer):** Custom pricing — not publicly disclosed. TokenSoft operates as a compliance-as-a-service provider with bespoke pricing based on project scope, number of recipients, chains supported, and compliance requirements. Foundation setup services also have variable pricing
- **Participant fee (buyer):** None documented — costs are borne by the issuing project, not recipients/investors
- **Listing/setup fee:** Custom — includes KYC/KYB setup, legal template preparation, smart contract deployment (ERC-1404), and compliance team onboarding. Foundation setup services (entity formation, governance, legal templates) priced separately. "Pricing may vary based on project need or situation"
- **Staking requirement:** None — access is compliance-based (KYC/KYB/accreditation), not token-based
- **Gas/proof costs:** EVM gas fees for token distribution, claims, and transfer restriction enforcement. Batch distribution supported to optimise gas costs for large recipient sets
- **Revenue model:** Enterprise SaaS model: (1) project setup/onboarding fees, (2) ongoing compliance management retainer, (3) foundation setup and administration services (entity formation, legal, directorship, compliance reporting), (4) API integration fees for ATS partners, (5) per-distribution or per-event fees for ongoing token operations

> [!analysis] TokenSoft's pricing is opaque and enterprise-oriented — likely in the $25k-$200k+ range for full-service compliance and distribution, based on industry norms for managed compliance platforms. Unlike Fjord or DAO Maker where pricing is transparent and percentage-based, TokenSoft's value proposition is reducing compliance risk and operational burden. Projects pay for the managed compliance team, not just the technology. This makes direct fee comparison difficult, but TokenSoft is clearly positioned for mid-to-large projects that need regulatory coverage rather than scrappy startups.

## Sale Lifecycle & Close Mechanics

> [!analysis] TokenSoft does not publish detailed sale lifecycle documentation; mechanics inferred from ERC-1404 standard, platform architecture, and enterprise compliance model

- **Manual close (issuer):** Yes — TokenSoft operates as a managed compliance service. The issuer (via TokenSoft's compliance team) can halt token distribution at any time by:
  - Removing addresses from the on-chain whitelist (blocking new claims)
  - Modifying ERC-1404 transfer restrictions to block all transfers
  - Pausing the distribution portal (platform-level)
  - Under applicable securities regulations, issuers can close offerings per the terms of their exemption (Reg D, SAFT, etc.)
- **Automatic close triggers:** (1) **All tokens distributed** — distribution/claim pool exhausted. (2) **Vesting schedule completion** — all tranches unlocked and claimed. (3) **Offering deadline** as specified in the offering documents. TokenSoft doesn't operate continuous sales — it manages structured distributions, so "close" typically means distribution completion.
- **Emergency halt/pause:** Yes — comprehensive freeze capability:
  - **On-chain:** ERC-1404 token contracts can restrict all transfers by modifying the whitelist or compliance rules. The contract admin can effectively freeze the token by clearing the whitelist or adding all addresses to a denylist.
  - **Platform-level:** TokenSoft's compliance team can halt the distribution portal, stopping all new claims.
  - **Who can trigger:** TokenSoft compliance team (as managed service provider), issuer (via TokenSoft), or regulatory authority.
- **Admin override:** Yes — TokenSoft holds admin keys for the ERC-1404 contracts it deploys. The contract admin role controls the whitelist, meaning TokenSoft can add/remove any address from the whitelist, effectively controlling all token transfers. This is a feature of the managed compliance model — the compliance team retains control.
- **Resume after pause:** Yes — whitelist modifications and transfer restriction changes are reversible. Addresses can be re-added to the whitelist, and compliance rules can be reverted. Platform distribution can also be restarted.
- **Post-close behavior:** Varies by offering:
  - **SAFT distributions:** Tokens distributed per vesting schedule, claimed through TokenSoft portal. Continuous transfer restrictions remain active post-distribution.
  - **Airdrops:** Batch distribution to verified addresses. Unclaimed tokens remain in the distribution contract.
  - **Ongoing compliance:** Unlike most platforms, TokenSoft's transfer restrictions are **permanent** (not just during the sale) — tokens can only ever be transferred between whitelisted addresses. This is a continuous compliance model, not a point-in-time sale.
- **Enforcement:** On-chain (ERC-1404 smart contract transfer restrictions) + off-chain (managed compliance service, portal access control). The on-chain enforcement is continuous — every token transfer is checked against the whitelist, making TokenSoft's enforcement the most persistent of the non-regulated platforms.

> [!analysis] TokenSoft's lifecycle model is distinct from launchpads — it's a distribution/compliance platform rather than a fundraising platform. The concept of "closing a sale" is less relevant; instead, TokenSoft manages ongoing token lifecycle with permanent transfer restrictions. The admin key control over ERC-1404 whitelists gives TokenSoft (and by extension, the issuer) complete power to freeze or restrict token transfers at any time, indefinitely. This is operationally similar to Securitize's DS Protocol but without the formal transfer agent registration.

## Open Questions
- Is TokenSoft's whitelist enforcement truly on-chain (Merkle proof or mapping) or does it rely on a centralised contract admin?
- Can ERC-1404 restrictions be combined with ZK proofs for privacy-preserving transfer compliance?
- What happens to whitelisted wallets if TokenSoft ceases operations — who controls the whitelist contract?

## Sources
- https://www.tokensoft.com/
- https://tokensoft.gitbook.io/tokensoft/api/use-cases
- https://tokenist.com/tokensoft-ceo-explains-security-token-whitelisting/
