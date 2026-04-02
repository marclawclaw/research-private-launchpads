---
topic: Hedgey Finance
type: competitor
tags: [vesting, lockup, EVM, Solana, free, token-infrastructure]
confidence: high
last_updated: 2026-04-02
sources:
  - https://hedgey.finance/
  - https://hedgey.finance/lockups
  - https://hedgey.finance/vesting
  - https://github.com/hedgey-finance/Locked_VestingTokenPlans
---

## Summary
Hedgey Finance is a free on-chain token infrastructure platform for vesting, investor lockups, grants, airdrops, and distributions. It positions itself as "100% free" with no protocol fees, targeting teams that need simple, secure token vesting without cost barriers. Supports EVM chains and Solana.

## Key Facts
- **Cost:** 100% free — no protocol fees, no platform fees, no subscription costs
- **Products:** Token vesting, investor lockups, grants, airdrops, token distributions
- **Chains:** Multiple EVM chains + Solana
- **Smart contracts:** Open-source (GitHub: hedgey-finance/Locked_VestingTokenPlans)
- **Features:** Vesting plans with cliff, start date (back/future-dated), revocable vesting (admin-controlled), transferable lockups (default), investor dashboard for tracking unlocks
- **Vesting Admin:** Role that can revoke plans (e.g., employee departure clawback)
- **Lockup Plans:** Non-revocable but transferable by default
- **Users:** Described as "trusted by the best" — used by multiple DeFi and Web3 projects

## Fee Structure

> [!fact] Confirmed from Hedgey Finance website (hedgey.finance, hedgey.finance/lockups, hedgey.finance/vesting)

- **Platform fee (issuer):** Zero — "100% free" for all features including vesting, lockups, grants, airdrops, and distributions
- **Participant fee (buyer/recipient):** Zero — no fees for recipients to claim, track, or interact with vesting plans
- **Listing/setup fee:** None
- **Staking requirement:** None — no native token required
- **Gas/proof costs:** Standard network gas fees (EVM or Solana) for creating vesting contracts and claiming tokens. This is the only cost
- **Revenue model:** Not publicly disclosed. Hedgey has received venture funding (Crunchbase profile exists). Likely monetisation paths include: (1) premium enterprise features or dashboards, (2) custom integrations/consulting, (3) future token launch, (4) data/analytics services, (5) ecosystem grants. The "free" model is a growth strategy to build adoption before monetising

> [!analysis] Hedgey is the only vesting platform that is genuinely 100% free at the protocol AND platform level. Unlike Sablier (free protocol but third-party integrators can charge broker fees), Hedgey has no fee mechanism at all — even for the official interface. This makes it the cheapest vesting option available, with costs limited to network gas fees. The risk is sustainability — without revenue, Hedgey depends on external funding. For projects choosing between vesting solutions: Hedgey = free + simple; Sablier = free protocol + NFT-based streams + more flexibility; Streamflow = cheap flat fees + Solana-native features.

## How it relates to Logos
- Hedgey's completely free model is a reference for how infrastructure can be offered as a public good
- Open-source vesting contracts could be adapted for privacy-preserving vesting in the Logos ecosystem
- The investor dashboard UX is a good reference for recipient-facing tools
- "Free" positioning creates adoption moats — relevant strategic consideration for any Logos vesting infrastructure

## Open Questions
- How does Hedgey sustain operations long-term without protocol fees?
- What is Hedgey's TVL (total tokens locked in vesting contracts)?
- Does Hedgey have audit reports for its smart contracts?
- Is there a planned token launch or monetisation roadmap?
- Hedgey experienced a significant exploit in April 2024 (~$44M in token approvals) — what is the current security posture?

## Sources
- https://hedgey.finance/
- https://hedgey.finance/lockups
- https://hedgey.finance/vesting
- https://github.com/hedgey-finance/Locked_VestingTokenPlans
