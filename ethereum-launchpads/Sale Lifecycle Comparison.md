---
topic: Sale Lifecycle & Close Mechanics
type: analysis
tags: [launchpad, lifecycle, close, pause, halt, refund, comparison]
confidence: high
last_updated: 2026-04-02
sources:
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
  - https://balancer.gitbook.io/balancer/guides/smart-pool-templates-gui/liquidity-bootstrapping-pool
  - https://developers.metaplex.com/smart-contracts/genesis
  - https://docs.sablier.com/support/faq
  - https://docs.streamflow.finance/en/articles/9674831-cancel-contract
  - https://github.com/hedgey-finance/Locked_VestingTokenPlans
  - https://github.com/securitize-io/dstoken
  - https://medium.com/securitize/ds-protocol-the-basic-elements-23fabcb5c85f
  - https://republic.com/help/can-i-close-my-campaign-early
  - https://github.com/tokensoft/tokensoft_token
---

# Sale Lifecycle & Close Mechanics — Cross-Protocol Comparison

## Summary

Comparison matrix of sale lifecycle controls (manual close, automatic triggers, emergency halt/pause, admin override, post-close behavior) across all studied launchpad, sale, and vesting protocols. Reveals a spectrum from fully centralized platform control (DAO Maker, Republic) to fully permissionless immutable contracts (Sablier, Metaplex Genesis).

## Comparison Matrix

> [!fact] Data compiled from official documentation, smart contract repos, and regulatory filings for each protocol

| Protocol | Manual Close (Issuer) | Auto-Close Triggers | Emergency Halt/Pause | Admin Override | Resume After Pause | Post-Close Behavior | Enforcement |
|----------|----------------------|--------------------|--------------------|---------------|-------------------|-------------------|-------------|
| **[[DAO Maker]]** | No — platform-controlled | Time window expiry | Platform-level only | Yes — full platform control | Yes | Manual claim; vesting per project; DYCO refund 16mo | Hybrid (off-chain alloc + on-chain claim) |
| **[[Fjord Foundry]]** | Partial — can pause swaps (LBP); cancel before start (FPS) | Time expiry; optional hardcap | Yes — creator pauses swaps | Not documented | Yes — pause is reversible | Manual claim; collateral to creator minus 5% fee | Hybrid (on-chain pause + platform UI) |
| **[[Balancer LBP]]** | Yes — pause swaps + remove liquidity | Weight schedule completion; time-based | Yes — pool controller (`canPauseSwapping`) | Limited — no per-pool governance override | Yes — `setSwapEnabled(true)` | Manual — creator removes liquidity + distributes | On-chain (smart contract) |
| **[[Polkastarter]]** | No evidence | Hardcap reached; time expiry | Not documented | Likely — platform deploys contracts | Unknown | Atomic swap — immediate token receipt | On-chain (swap) + off-chain (allowlist) |
| **[[Securitize]]** | Yes — Transfer Agent freeze | Max raise cap; offering deadline; compliance failure | Yes — multi-layer (contract, compliance, platform, SEC) | Yes — comprehensive (Transfer Agent role) | Yes — freeze is reversible | Varies: claim portal, secondary trading, Reg CF refund | On-chain (DS Protocol) + off-chain (platform) |
| **[[Republic]]** | Yes — with regulatory constraints (Reg CF: 5-day notice after target) | Target reached; max cap; deadline; target not met → refund | Yes — FINRA obligation on fraud/misrep | Yes — full platform + SEC | Depends on cause | Escrow release; refund if target not met; 1yr resale lock | Off-chain (platform + regulatory) |
| **[[TokenSoft]]** | Yes — whitelist removal + ERC-1404 restrictions | All tokens distributed; vesting complete; deadline | Yes — contract freeze + platform halt | Yes — holds admin keys for ERC-1404 | Yes — whitelist reversible | Claim portal; permanent transfer restrictions | Hybrid (on-chain ERC-1404 + platform) |
| **[[Metaplex Genesis]]** | No documented early close | Deposit window closes (time-based) | Not documented | Limited — no per-launch override | N/A | Auto-distribute proportional (Launch Pool); FCFS (Presale); refund if goal not met | On-chain (Solana program) |
| **[[Streamflow Finance]]** | Yes — configurable cancellation | Vesting schedule completion | Cancellation only (no pause) | Limited — per-contract permissions | No — cancellation is permanent | Unlocked → recipient; locked → sender; 1.70% clawback fee | On-chain (Solana/EVM smart contract) |
| **[[Sablier Protocol]]** | Yes — cancel (Lockup) or void (Flow) | Stream end time; all tokens withdrawn | Lockup: cancel only; Flow: pause/void | None — fully permissionless, no admin | Flow: yes (pause→restart); Lockup: no | Streamed → recipient; unstreamed → sender | On-chain (EVM smart contract) |
| **[[Hedgey Finance]]** | Yes — Vesting Admin revocation | Vesting schedule completion | Revocation serves as halt (no pause) | Scoped to Vesting Admin only; no platform override | No — revocation is permanent | Unvested → admin; vested → beneficiary claimable | On-chain (EVM smart contract) |

## Key Patterns

> [!analysis] Patterns identified from cross-protocol comparison

### 1. Centralization Spectrum

```
Most Centralized ←————————————————————————→ Most Decentralized
DAO Maker → Republic → Securitize → TokenSoft → Fjord → Polkastarter → Balancer LBP → Streamflow → Hedgey → Metaplex Genesis → Sablier
```

- **Fully centralized** (DAO Maker, Republic): Platform controls entire lifecycle; no on-chain autonomy for issuers
- **Regulated hybrid** (Securitize, TokenSoft): On-chain enforcement + platform/regulatory overlay; strongest halt capabilities
- **Creator-controlled** (Fjord, Balancer LBP): Smart contract gives creator pause/resume; platform adds UI layer
- **Permissionless immutable** (Sablier, Metaplex Genesis): Parameters locked at creation; no admin override possible

### 2. Pause vs Cancel — No Middle Ground

Most protocols offer either:
- **Reversible pause** (Fjord, Balancer LBP, Sablier Flow): Temporarily halt, resume later
- **Permanent cancellation** (Streamflow, Hedgey, Sablier Lockup): Terminate and split funds

Only **Securitize** and **TokenSoft** offer both pause (freeze) AND resume across the full token lifecycle — because regulatory compliance requires it.

### 3. Post-Close Behavior Patterns

| Pattern | Protocols | Description |
|---------|-----------|-------------|
| **Atomic swap** | Polkastarter | Tokens delivered instantly during sale — no post-close step |
| **Manual claim** | DAO Maker, Fjord, TokenSoft | Participants must actively claim tokens after sale closes |
| **Proportional distribution** | Metaplex Genesis (Launch Pool) | Automated on-chain proportional split based on deposits |
| **Stream settlement** | Sablier, Streamflow | Vested portion to recipient, unvested to sender |
| **Escrow release** | Republic | Off-chain funds released from escrow to issuer |
| **Mandatory refund** | Republic (Reg CF), Metaplex Genesis (failed goal) | Automatic return of funds if minimum not met |

### 4. Regulatory Influence on Close Mechanics

- **Reg CF** (Republic): SEC mandates 5-day notice for early close, investor cancellation rights, mandatory refund on target miss
- **Securities** (Securitize, TokenSoft): Transfer Agent/compliance role legally required to maintain halt capability
- **Crypto-native** (all others): No regulatory requirement for close/halt — design choices driven by trust model

### 5. Logos Launchpad Implications

> [!analysis] Design considerations for a privacy-preserving launchpad

1. **Minimum viable controls:** A credible launchpad needs at least: time-based auto-close + issuer cancel/pause + post-close claim mechanism
2. **Privacy vs halt capability:** ZK-based sales could make emergency halts difficult — if participant identities are hidden, targeted freezes (Securitize-style) are impossible without breaking privacy
3. **The Sablier model is most aligned** with Logos values: fully permissionless, no admin keys, immutable parameters — but this sacrifices all emergency intervention capability
4. **Hybrid approach needed:** On-chain immutable sale parameters (Metaplex Genesis model) + optional creator-controlled pause (Balancer LBP model) + privacy-preserving participant claims
5. **Refund mechanisms require identity linkage** — privacy-preserving refunds (prove you participated without revealing identity) would be a novel contribution

## How it relates to Logos

A Logos-native launchpad must navigate the tension between:
- **Decentralization** (no admin override, immutable parameters) — Sablier/Metaplex Genesis model
- **Issuer protection** (ability to halt if something goes wrong) — Balancer LBP pause model
- **Regulatory compliance** (halt capabilities for regulated offerings) — Securitize/Republic model
- **Privacy** (hidden participants, confidential amounts) — none of the existing platforms

The ideal architecture: immutable sale parameters set at creation (time windows, caps), optional issuer-controlled pause (on-chain, transparent), ZK-proof-based claims (private participation), and cryptographic refund proofs (if sale fails).

## Open Questions

- Can a ZK-proof system enable emergency halts without revealing participant identities?
- How would a privacy-preserving refund work if the sale fails to meet its minimum?
- Is there demand for regulated (Reg D/CF) offerings with privacy-preserving participation?
- Could a Balancer LBP-style pause mechanism work with confidential swap amounts?

## Sources

- Fjord Foundry LBP FAQ: https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
- Balancer v1 LBP docs: https://balancer.gitbook.io/balancer/guides/smart-pool-templates-gui/liquidity-bootstrapping-pool
- Metaplex Genesis docs: https://developers.metaplex.com/smart-contracts/genesis
- Sablier FAQ: https://docs.sablier.com/support/faq
- Streamflow Cancel Contract: https://docs.streamflow.finance/en/articles/9674831-cancel-contract
- Hedgey Vesting Plans (GitHub): https://github.com/hedgey-finance/Locked_VestingTokenPlans
- Securitize DS Protocol: https://medium.com/securitize/ds-protocol-the-basic-elements-23fabcb5c85f
- Securitize DSToken v4 (GitHub): https://github.com/securitize-io/dstoken
- Republic early close help: https://republic.com/help/can-i-close-my-campaign-early
- TokenSoft token contracts (GitHub): https://github.com/tokensoft/tokensoft_token
