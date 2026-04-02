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

## Sale Lifecycle & Close Mechanics

> [!fact] Confirmed from Hedgey Finance GitHub (hedgey-finance/Locked_VestingTokenPlans README), app.hedgey.finance/vesting, and Filecoin devgrant description

- **Manual close (issuer):** Yes — **Vesting Plans are revocable by the Vesting Admin**:
  - Each Vesting Plan has a designated **Vesting Admin** (set at creation, typically the issuing project/team) who has the authority to revoke the plan at any time.
  - On revocation: unvested tokens are returned to the Vesting Admin; vested tokens remain claimable by the beneficiary (recipient).
  - **Lockup Plans** (for investors): non-revocable by default. However, Lockup Plans are transferable (the NFT can be sold/transferred), giving recipients flexibility without giving issuers clawback rights.
- **Automatic close triggers:** (1) **Vesting schedule completion** — all tokens vest per the configured schedule (linear with optional cliff and periodic unlocks). (2) **All tokens redeemed** — when the beneficiary has claimed all vested tokens, the plan is functionally complete. No documented external triggers.
- **Emergency halt/pause:** The revocation function serves as an emergency halt for Vesting Plans — the Vesting Admin can revoke at any time, including immediately. There is no separate "pause then resume" mechanism for vesting — revocation is the only admin intervention. The Vesting Admin role is the sole emergency control; there is no platform-level (Hedgey team) override for individual plans.
- **Admin override:** Scoped to Vesting Admin role only. Hedgey Finance (the company) does not retain admin keys over deployed vesting contracts. The Vesting Admin is the project/issuer who created the plans. This is confirmed by the open-source contract architecture — no upgradeable proxy, no platform multisig in the vesting logic.
  - **Note:** The April 2024 exploit ($44M in token approvals drained) was via the `cancelCampaign` function in the (separate, now-deprecated) ClaimCampaigns.sol contract — the exploit did NOT affect Vesting Plans or Lockup Plans.
- **Resume after pause:** Not applicable — there is no pause mechanism. Revocation is permanent. After revocation, a new vesting plan must be created to resume vesting for a recipient.
- **Post-close behavior:**
  - On revocation: unvested tokens return to Vesting Admin; vested tokens remain available for beneficiary to claim (no expiry documented).
  - On natural completion: beneficiary redeems all tokens per schedule; partial redemptions supported.
  - NFT-based: each plan is an ERC-721 NFT owned by the beneficiary. Lockup Plan NFTs are transferable by default; Vesting Plan NFTs are also transferable (enabling OTC secondary market for vesting positions). Bound variants (non-transferable) available.
  - Voting with locked tokens: plans support Snapshot and on-chain governance voting with unvested/unlocked tokens.
- **Enforcement:** On-chain (EVM smart contracts). Revocation is a smart contract transaction executed by the Vesting Admin wallet. The vesting schedule (cliff, start date, period, unlock amount) is stored on-chain in the NFT state. No platform intermediary required for execution — direct smart contract interaction is possible. Audited (3 audits post-2024 exploit with no critical findings on core contracts).

> [!analysis] Hedgey's revocation model closely mirrors Sablier's cancelable Lockup streams — the issuer can reclaim unvested tokens (e.g., employee departure) but cannot touch already-vested tokens. The key difference is that Hedgey explicitly separates Vesting Plans (revocable, for employees/contributors) from Lockup Plans (non-revocable, for investors), which is a useful design pattern. Lockup Plans being non-revocable but transferable is an elegant investor protection: investors can't be rug-pulled, but they can exit via secondary market (selling the NFT). The 2024 exploit's origin in a separate (now deprecated) campaign contract, not the core vesting logic, is an important nuance.

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
