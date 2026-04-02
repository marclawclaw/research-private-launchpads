---
topic: Republic
type: competitor
tags: [ethereum, crowdfunding, reg-cf, reg-d, permissioned, kyc, compliance, token-dpa]
confidence: high
last_updated: 2026-04-02
sources:
  - https://republic.com/
  - https://republic.com/token-dpa
  - https://republic.com/help/why-do-i-have-to-verify-my-identity-or-go-through-kyc-3
  - https://republic.com/help/do-i-have-to-be-accredited-to-invest-1
---

## Summary
Republic is a FINRA-registered funding portal and broker-dealer that enables both retail and accredited investor participation in token raises via Reg CF, Reg D, Reg A+, and Reg S exemptions. Access control is entirely regulatory-driven: investor qualification, KYC/AML, and investment limits are enforced by the platform as legal requirements, not as optional features.

## Key Facts
- Founded 2016; hundreds of successful raises across equity and crypto
- Products: Token DPA (Deferred Purchase Agreement under Reg CF), Mirror Tokens (Reg D), traditional equity raises
- Reg CF raises: up to $5M, open to all investors (accredited + non-accredited)
- Reg D raises: accredited investors only, no cap
- Reg A+: up to $75M, open to all investors
- Platform handles all KYC/AML, investor qualification, and ongoing SEC reporting
- Consumer-friendly UI with both retail and accredited investor portals
- Mobile app available

## Allowlist & Access Control

> [!fact] Confirmed from Republic help center, SEC regulations, and Republic Token DPA documentation

- **Gating method:** Mandatory KYC/AML + regulatory investor qualification (accredited/non-accredited status determines access). No token staking or lottery — access is purely regulatory
- **Enforcement:** Off-chain (platform-level). Republic, as a registered intermediary, enforces all access control:
  - KYC/identity verification required for all investors
  - Accredited investors must: (1) complete subscription agreement, (2) acknowledge Private Placement Memorandum, (3) provide accreditation verification (income/net worth documentation or professional certification)
  - Non-accredited investors: verified by platform, subject to SEC-mandated investment limits
  - No on-chain enforcement of access control — compliance is managed at the platform layer before any on-chain token interaction
- **Tiered access:** Yes — regulatory tiers:
  - **Non-accredited (Reg CF):** Can invest, but subject to annual investment limits based on lesser of annual income and net worth. Minimum investment as low as $10
  - **Accredited (Reg D):** No investment limits. Access to all offerings including Reg D-only deals
  - **Qualified purchasers:** Access to institutional-grade offerings
  - Some deals are Reg D-only (accredited exclusively); all Reg CF and Reg A+ deals are open to both
- **Geo-blocking:** Yes — US-centric platform. Reg CF and Reg D are US securities exemptions; non-US investors may participate under Reg S but with separate compliance requirements. Republic enforces jurisdictional restrictions at the platform level
- **Phased rounds:** Yes — projects can run multiple rounds:
  - Community round (Reg CF) → Accredited round (Reg D) → Institutional round
  - 48-hour cancellation window mandated by SEC for Reg CF (investors can cancel for any reason up to 48h before deadline)
  - If target amount not met, all commitments cancelled and funds returned (mandatory soft cap)
- **Sybil resistance:** Very strong — regulated intermediary model:
  - Full identity verification (government ID, address, SSA) required
  - One account per person enforced by FINRA-registered platform
  - Accredited status requires documentary proof
  - Platform monitors for suspicious activity as required by AML regulations
  - Securities cannot be resold for 1 year (Reg CF), preventing quick flip attacks

> [!analysis] Republic's access control model is the regulatory gold standard — every protection is mandated by law, not optional. The 48-hour cancellation right, mandatory soft caps, and material change re-confirmation (see [[Regulation CF]]) provide the strongest investor protection of any platform studied. The tradeoff is complete centralisation: Republic is a mandatory intermediary, and there is zero privacy — all investor PII is held by the platform and reportable to the SEC. For Logos, Republic demonstrates that regulatory compliance and broad access (including non-accredited investors) are compatible, but the intermediary requirement conflicts with permissionless ethos.

See also: [[Regulation CF]], [[Regulation D]], [[On-Chain KYC Providers]]

## How it relates to Logos
- Reg CF model shows a path to retail participation in token raises with regulatory cover — relevant for Logos ecosystem projects targeting US community
- Token DPA instrument is a legal innovation for selling rights to future tokens to non-accredited investors
- Republic's centralised model is the problem Logos could solve: ZK-proof accreditation + on-chain compliance could remove the intermediary requirement
- Mirror Tokens concept (tokenized exposure to private shares) could be implemented with privacy using Logos stack

## Fee Structure

> [!fact] Confirmed from Republic official help page, Business.org review, OpenVC, and Scoutmine cost comparison

- **Platform fee (issuer):** 6% of total amount raised in cash + 2% of securities offered (equity or tokens). Some sources cite 7% cash + 2% securities for certain offering types. This is a success fee — charged only on completed raises
- **Participant fee (buyer):** None — Republic charges zero fees to investors. All costs are borne by the issuer
- **Listing/setup fee:** $0-$3,500 for attorney/legal review (optional if issuer has own counsel). Republic's legal partners offer flat-fee Form C compliance and review. UK/EU operations may charge £5k pre-registration + £5k launch fee + £2k annual nominee fee
- **Staking requirement:** None — access is regulatory-based (KYC/accreditation), not token-based
- **Gas/proof costs:** Minimal — Republic handles most operations off-chain. Token DPA (Deferred Purchase Agreement) doesn't require on-chain interaction until token delivery
- **Revenue model:** (1) Success-based commission (6% cash + 2% securities) on every completed raise, (2) legal/advisory fees for offering structuring, (3) Republic Capital (in-house VC fund) co-investing in deals, (4) Republic Note (tokenized revenue share instrument), (5) managed services for ongoing SEC reporting and compliance

> [!analysis] Republic's 6%+2% fee structure is the industry standard for regulated crowdfunding portals (Wefunder charges 7.5%, StartEngine charges 7-12%). The 2% securities component means Republic has equity/token upside in every deal — an alignment incentive. Zero investor fees and low setup costs ($0-3.5k) make it accessible for early-stage projects, but the 6% success fee is significant for larger raises. At $5M (Reg CF max), Republic would earn $300k in cash fees plus 2% of securities.

## Open Questions
- Can a ZK-proof accredited investor attestation satisfy SEC's "reasonable steps" requirement under Rule 506(c)?
- Is it possible to run a Reg CF raise with a decentralised funding portal (smart contract as intermediary)?
- How does Republic handle cross-border Reg CF + Reg S hybrid offerings?

## Sources
- https://republic.com/
- https://republic.com/token-dpa
- https://republic.com/help/why-do-i-have-to-verify-my-identity-or-go-through-kyc-3
- https://republic.com/help/do-i-have-to-be-accredited-to-invest-1
- https://republic.com/help/what-is-an-accredited-investor
