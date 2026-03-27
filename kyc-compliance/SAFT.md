---
topic: SAFT (Simple Agreement for Future Tokens)
type: concept
tags: [compliance, fundraising, securities, saft, token-sale]
confidence: high
last_updated: 2026-03-27
sources:
  - https://qubit.capital/blog/token-sales-regulations
  - https://sumsub.com/blog/kyc-legal-for-sto/
---

## Summary
The SAFT (Simple Agreement for Future Tokens) is a contractual instrument used by blockchain startups to raise capital before network launch. It treats the initial sale as a securities offering (typically under Reg D), deferring token delivery until the protocol is functional and the token may no longer qualify as a security.

## Key Facts
- Investors purchase rights to future tokens; delivery contingent on network launch
- Commonly structured under Reg D Rule 506(c) — accredited investors only, general solicitation allowed
- Pioneered by Filecoin (~$200M raise in 2017 under Rule 506(c))
- The SAFT itself is a security; the delivered token may or may not be
- Requires transparent disclosure: token economics, vesting schedules, risk factors
- Form D must be filed electronically with SEC after first sale
- Securities purchased are "restricted" — cannot be resold for 6–12 months without registration

> [!fact] Confirmed from qubit.capital and sumsub.com
> Filecoin raised over $200M via SAFT under Rule 506(c). SAFT does not guarantee the eventual token is not a security.

> [!analysis] The SAFT framework is increasingly being supplemented or replaced by Token DPAs (Deferred Purchase Agreements) such as used by Republic.

## How it relates to Logos
- If Logos ecosystem projects pursue US fundraising, SAFT under Reg D 506(c) is a viable path for accredited-only raises
- Privacy-preserving KYC attestations could underpin accredited investor verification without revealing investor PII on-chain
- Logos' privacy stack (e.g. Waku, Nomos) could support confidential SAFT investor record-keeping

## Open Questions
- Does the delivered Logos-ecosystem token qualify as a utility (non-security) token post-launch?
- Can ZK proofs replace traditional accredited investor verification ("reasonable steps") under 506(c)?
- How does SAFT interact with non-US jurisdictions (EU MiCA, Singapore MAS)?

## Sources
- https://qubit.capital/blog/token-sales-regulations
- https://sumsub.com/blog/kyc-legal-for-sto/
- https://www.moschettilaw.com/raising-capital-for-crypto-blockchain-projects-under-reg-d/
