# KYC-Gated / Accredited Investor Token Sales & Compliance

**Folder:** `kyc-compliance/`  
**Phase:** 2 — Deep Crawl complete  
**Last updated:** 2026-03-27  
**Researcher:** Marclaw researcher agent

---

## Notes

| File | Type | Summary |
|------|------|---------|
| [SAFT.md](./SAFT.md) | concept | Simple Agreement for Future Tokens — contractual instrument for pre-launch fundraising under Reg D; defers token delivery until network is live |
| [Regulation D.md](./Regulation%20D.md) | concept | Primary SEC private offering exemption for token sales; 506(b) vs 506(c) — accredited investor verification requirements |
| [Regulation CF.md](./Regulation%20CF.md) | concept | Reg Crowdfunding — raises up to $5M from accredited + non-accredited via registered portal; used by Republic.co Token DPA |
| [On-Chain KYC Providers.md](./On-Chain%20KYC%20Providers.md) | concept | ERC-3643, Sumsub, Securitize, Republic, Synaps — how KYC is enforced at the token transfer layer |
| [SEC Crypto Disclosure Guidance 2025.md](./SEC%20Crypto%20Disclosure%20Guidance%202025.md) | concept | April 2025 SEC Corp Fin guidance on disclosure for crypto securities offerings (Form S-1, Reg A, etc.) |

---

## Key Themes

1. **Two fundraising tiers**: Reg D 506(c) for large accredited-only raises (no cap); Reg CF for community raises (≤$5M, non-accredited allowed)
2. **SAFT bridges pre-launch fundraising**: The token agreement is the security; the delivered token may not be
3. **On-chain compliance is maturing**: ERC-3643 enables transfer-level enforcement; Securitize demonstrated this at scale with BlackRock's BUIDL fund
4. **KYC providers are a commodity**: Sumsub, Synaps, Parallel Markets all do accredited verification; the differentiator is on-chain integration quality
5. **Privacy gap**: No mainstream solution for ZK-based accredited investor proofs; this is a design opportunity for Logos

---

## Logos Opportunity

> [!analysis] Logos ecosystem has a strong fit here: privacy-preserving KYC attestations using ZK proofs could satisfy regulatory "reasonable steps" requirements without exposing investor PII on-chain. ERC-3643's claim-issuer architecture is the natural integration point.

---

## Sources Crawled

- https://qubit.capital/blog/token-sales-regulations
- https://sumsub.com/blog/kyc-legal-for-sto/
- https://www.sec.gov/newsroom/speeches-statements/cf-crypto-securities-041025-offerings-registrations-securities-crypto-asset-markets
- https://republic.com/token-dpa
- https://build.avax.network/integrations/securitize
- https://www.chainalysis.com/blog/introduction-to-erc-3643-ethereum-rwa-token-standard/
- https://www.erc3643.org/news/erc-3643-presented-to-the-sec-crypto-task-force
- https://docs.erc3643.org/erc-3643
- https://www.crowdfundinsider.com/2026/01/257409-republic-shares-update-on-2025-activities/
- https://www.bny.com/corporate/global/en/about-us/newsroom/company-news/securitize-launches-tokenized-aaa-clo-fund-with-services-provided-by-bny-bringing-institutional-structured-credit-on-chain.html
