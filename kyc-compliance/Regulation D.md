---
topic: Regulation D (Reg D)
type: concept
tags: [compliance, securities, regulation, accredited-investor, token-sale, US]
confidence: high
last_updated: 2026-03-27
sources:
  - https://qubit.capital/blog/token-sales-regulations
  - https://sumsub.com/blog/kyc-legal-for-sto/
---

## Summary
Regulation D is the primary SEC exemption used by US blockchain startups to conduct private token sales without full securities registration. It has two main rules relevant to token sales: 506(b) (no general solicitation, up to 35 non-accredited investors) and 506(c) (general solicitation allowed, accredited investors only with verified status).

## Key Facts
- **Rule 504**: Exempts up to $10M in 12 months; no restriction on investor type
- **Rule 506(b)**: Unlimited accredited investors + up to 35 non-accredited (sophisticated); NO general solicitation; investors self-verify accredited status
- **Rule 506(c)**: Unlimited accredited investors ONLY; general solicitation/advertising allowed; issuer must take "reasonable steps" to verify accredited status
- No cap on raise amount under 506(b) or 506(c)
- Must file **Form D** electronically with SEC after first sale
- Securities are "restricted" — resale restricted for 6–12 months
- Platforms: AngelList, FundersClub used for Reg D token raise management

> [!fact] Confirmed — SEC and multiple legal sources
> 506(c) is the preferred route for public-marketing token sales; requires active KYC/accreditation verification (not just self-certification).

> [!analysis] 506(c) creates the strongest demand for on-chain or API-based KYC/accreditation checks because issuers bear the verification burden.

## How it relates to Logos
- Reg D 506(c) is the dominant framework for institutional/accredited token raises in the US
- On-chain KYC attestations (e.g. via [[ERC-3643]] or Sumsub) could satisfy "reasonable steps" for accredited verification
- Logos privacy tools could enable compliant investor identity proofs without exposing PII to the chain

## Open Questions
- What constitutes "reasonable steps" for on-chain accredited investor verification in 2025?
- Can a ZK credential (proving net worth > $1M without revealing it) satisfy 506(c)?
- Does transferring a Reg D token via a DEX trigger resale restriction violations?

## Sources
- https://qubit.capital/blog/token-sales-regulations
- https://sumsub.com/blog/kyc-legal-for-sto/
- https://www.sec.gov/files/ctf-written-input-securitize-050725.pdf
