---
topic: Penumbra Shielded Staking
type: concept
tags: [penumbra, staking, delegation-token, lsd, privacy, token-issuance]
confidence: high
last_updated: 2026-03-27
sources:
  - https://protocol.penumbra.zone/main/index.html
  - https://penumbra.zone/blog/shielded-staking-on-penumbra
---

## Summary
Penumbra's staking mechanism issues per-validator delegation tokens representing shares in a shielded delegation pool. These tokens are first-class shielded assets (recorded in the multi-asset shielded pool), enabling private staking derivatives and serving as a concrete example of ZK-native token issuance.

## Key Facts
- **Mechanism:** No explicit staking rewards — instead, an epoch-varying exchange rate between the staking token and each validator's delegation token prices in the reward
- **Fungibility:** All delegations to a single validator are fungible — one delegation token type per validator
- **Private issuance:** Delegation tokens are minted and recorded in the shielded pool; delegator privacy is preserved while validator accountability (total stake, consensus weight) remains public
- **LST-native:** Stake is already tokenized by design — stake pools just need to pool these tokens, no multisig trust assumptions needed
- **Tax efficiency:** Delegators realize capital gain/loss on unbonding, not income during bonding — relevant for tax-compliant private staking
- **Governance:** Delegators vote secretly using zero-knowledge proofs of stake ownership; votes encrypted to threshold key

## How it relates to Logos
- Penumbra demonstrates that protocol-level token issuance (delegation tokens) can be fully private — a model for Logos token distribution where initial allocations to stakeholders are not publicly visible
- The exchange-rate reward mechanism (no explicit mint events) is cleaner from a privacy standpoint than inflation-based staking — avoids revealing reward amounts
- Private governance voting (ZK proof of stake ownership) is directly applicable to Logos DAO mechanics

> [!fact] Delegation tokens can be traded and transacted with like any other asset within the shielded pool, making them liquid staking derivatives by default — no additional protocol needed.

## Open Questions
- What happens to delegation token privacy if a validator is slashed?
- Can external parties (e.g., a launchpad) issue custom tokens into Penumbra's shielded pool, or only IBC-bridged assets and delegation tokens?

## Sources
- https://protocol.penumbra.zone/main/index.html
- https://penumbra.zone/blog/shielded-staking-on-penumbra
- https://mirror.xyz/a20z.eth/uzqgNjngKnX6VsVJ7OfJ2e0yIcyswbopAQGQsb6fFQs
