---
topic: Aztec Governance Model
type: concept
tags: [aztec, governance, decentralization, upgrade-process]
confidence: high
last_updated: 2026-03-27
sources:
  - https://aztec.network/blog/how-aztec-governance-works
---

## Summary
Aztec uses a two-layer on-chain governance system (AZIP + AZUP) where protocol upgrades require sequencer signaling followed by a supermajority tokenholder vote. No single party — including the core team — can force or block an upgrade.

## Key Facts
- **AZIP (Aztec Improvement Proposal):** Version-controlled design docs on GitHub, modeled on EIPs. Lifecycle: Draft → Ready for Discussion → Accepted/Rejected. Rejected AZIPs are kept permanently.
- **AZUP (Aztec Upgrade Proposal):** Bundles an accepted AZIP into an on-chain payload encoding exact smart contract changes. Publicly inspectable on block explorer before vote.
- **Sequencer signaling:** Sequencers must accumulate quorum of signals for a proposal to advance. Sequencers' staked voting power defaults to "yea" — opposition must actively re-delegate.
- **Tokenholder vote:** After sequencer signaling, tokenholders vote. Must meet quorum + supermajority + minimum participation — all three.
- **Mandatory delay post-vote:** Node operators time to deploy; grace period; no execution if expired.
- **Failed AZUPs cannot be resubmitted** — a new proposal addressing feedback is required.
- **Security mandatory** for Core/Standard/Economics AZIPs — can't pass Draft without it.

## How it relates to Logos
- Reference model for decentralized protocol governance that separates infrastructure operators (sequencers) from token holders
- The "default yea with active opposition" sequencer vote design is worth studying for any Logos governance module

> [!analysis] Aztec's governance is stronger than most L2s — no admin key, no team veto. This is a meaningful signal for institutional adoption of private DeFi.

## Open Questions
- Have any AZUPs been proposed/passed since Mainnet launch?
- How is quorum defined — by staked weight or by count of sequencers?

## Sources
- https://aztec.network/blog/how-aztec-governance-works
- https://github.com/AztecProtocol/governance
