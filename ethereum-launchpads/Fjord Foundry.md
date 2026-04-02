---
topic: Fjord Foundry
type: competitor
tags: [ethereum, launchpad, lbp, token-sale, permissioned]
confidence: high
last_updated: 2026-04-02
sources:
  - https://www.fjordfoundry.com/
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
---

## Summary
Fjord Foundry is an Ethereum-based token sale platform specialising in Liquidity Bootstrapping Pools (LBPs). It supports both permissionless community sales (upvote-gated) and curated/partnered sales backed by Fjord or trusted launch partners. Optional whitelisting feature restricts participation to a curated participant list.

## Key Facts

### Scale & Traction

> [!fact] Confirmed from Bitbond review (Sep 2025)
> - **Total funds raised across all LBPs:** >$1 billion
> - **Total swap volume:** >$1.5 billion
> - **Total LBPs launched:** 717
> - **Total participants:** 106,762
> - **Total fees generated:** $30 million
> - **Own FJO token LBP:** raised $15.3M (April 2024, highest single LBP raise of 2024)

### Mechanism
- Primary mechanism: LBPs (dynamic pricing, price starts high and decreases over time based on weight shifts)
- Two sale tiers: permissionless (community upvote) vs. curated/partnered (Fjord or launch partner backed)
- Optional whitelist: project creators can enable participant whitelisting for exclusivity
- Fee: 5% of collateral raised
- Supports zero-liquidity LBPs (synthetic/virtual collateral to generate price curve; no upfront deposit required)
- Supports buy-only or buy+sell LBP modes
- Hard cap configurable; no per-wallet limits for LBPs
- Sale duration: typically 2–5 days (3 days recommended)
- Recommended weight structure: 99/1 → 1/99 (100% token distribution target); starting price ~6–8× fair value to deter bots
- $FJO native token — NOT used to gate sales (explicit ethos: open access, no token-gating)
- Own LBP raised $15M+ in April 2024; $FJO down 70% from peak as of late 2025
- Chains: Ethereum (and others — multi-chain)
- Previously merged with Copper.co (rebranded)

## How it relates to Logos
- LBP mechanism is a model for fair, permissionless token distribution — relevant to Logos ecosystem projects needing price discovery without pre-set valuations
- Optional whitelisting feature = permissioned layer on top of open infrastructure; useful reference for hybrid open/gated designs
- Zero-liquidity LBPs lower barrier to entry for early-stage projects

> [!analysis] Fjord explicitly rejects token-gating on their own platform, distinguishing themselves from Polkastarter/DAO Maker tier models. Permissioning is optional, project-side.

## Refund & Participant Protection

> [!analysis] No native refund mechanism — LBP purchases are market trades, not subscriptions

- **Refund window:** No. LBP purchases are AMM swaps — once executed, they are final. There is no post-purchase refund window or grace period.
- **Minimum raise threshold (soft cap):** No. LBPs have no minimum raise requirement. The sale runs regardless of how much capital is deposited. If demand is low, the price simply falls to meet it.
- **Post-launch performance refund:** No. LBP tokens are freely traded on the AMM during the sale. Participants can sell back during the sale window if it's configured as buy+sell mode, but this is a market transaction at current AMM price, not a guaranteed refund.
- **Cancellation rights:** Limited. During the LBP, participants can sell tokens back into the pool (if buy+sell mode is enabled), but at market price — not at their purchase price. After the LBP ends, tokens are distributed and there is no platform-level refund mechanism.

> [!analysis] The LBP's declining-price mechanism provides *implicit* buyer protection: since price starts high and falls over time, patient buyers get better prices. Early buyers who overpay can sell back during the sale at market price, but this is not a guaranteed refund. Fjord's vesting feature (optional cliff + linear vesting post-LBP) locks tokens, further removing any post-sale refund possibility.

## Allowlist & Access Control

> [!fact] Confirmed from Fjord Foundry docs (tiered sale guide, LBP FAQ) and Bitbond review

- **Gating method:** Optional project-managed whitelist (address-based CSV upload) OR fully open (no gating). Fjord explicitly rejects platform-level token-gating — $FJO is NOT required to participate
- **Enforcement:** Off-chain (platform-level). Project creators upload a CSV of whitelisted wallet addresses during sale setup. Enforcement appears to be at the Fjord platform/UI layer, not via on-chain Merkle proofs. No evidence of on-chain whitelist contracts
- **Tiered access:** Yes — Fjord supports tiered fixed-price sales with per-tier configuration:
  - Each tier can have different token amounts for sale and price per token
  - Minimum and maximum allocation per user configurable per tier
  - Tiers are project-defined, not platform-wide (unlike DAO Maker's universal tier system)
  - LBPs themselves have no per-wallet limits or tiered access
- **Geo-blocking:** Yes — project creators can specify "Geo-blocked Countries" during sale setup to restrict participation by region. Enforcement is at the platform level
- **Phased rounds:** Yes — tiered sales support Seed, Private, and Public round types. LBPs are typically single-phase but the declining-price curve creates an implicit time-gated advantage for patient buyers
- **Sybil resistance:** Weak for LBPs (open access, no identity verification). For whitelisted tiered sales, Sybil resistance depends on how the project curates the whitelist (Fjord provides the tool, not the curation). Anti-Snipe feature can be enabled to prevent bot participation. No mandatory KYC at the platform level

> [!analysis] Fjord's permissioning philosophy is fundamentally different from DAO Maker/Polkastarter: access control is a project-side option, not a platform-enforced requirement. This makes Fjord maximally flexible but means Sybil resistance is only as strong as each project's whitelist curation process. The LBP mechanism's anti-bot properties (high starting price, declining curve) provide structural protection but not identity-level Sybil resistance.

See also: [[Token Sale Permissioning Mechanisms]], [[Liquidity Bootstrapping Pool (LBP)]]

## Fee Structure

> [!fact] Confirmed from Fjord Foundry docs, platform FAQ, and DefiLlama fee tracking

- **Platform fee (issuer):** 5% of collateral raised — deducted from proceeds at the end of the LBP or fixed-price sale. No upfront cost to launch
- **Participant fee (buyer):** None — no additional fee charged to buyers beyond the LBP swap price. Standard AMM swap fees may apply (configurable by sale creator, typically 1-2%, max 10%)
- **Listing/setup fee:** None for permissionless (community upvote) sales. Curated/partnered sales may involve partnership agreements but no published upfront fee
- **Staking requirement:** None — $FJO token is explicitly NOT required to participate in sales. Fjord's ethos rejects token-gating
- **Gas/proof costs:** Standard Ethereum gas fees borne by participants for swap transactions. Multi-chain deployment reduces gas costs on L2s
- **Revenue model:** Platform fee (5% of collateral) is the primary revenue source. $FJO token provides governance but not sale access. Fjord raised $15M+ via its own LBP in April 2024

> [!analysis] Fjord's 5% fee on collateral raised is competitive and transparent — comparable to DAO Maker's 5% but without the additional participant-side fees (DAO Maker charges 5-30% on the buyer side). The zero-barrier-to-entry for both projects and participants makes Fjord one of the lowest-friction launchpads. However, since fees are only collected on successful raises, Fjord's revenue is highly dependent on market activity and launch volume.

## Sale Lifecycle & Close Mechanics

> [!fact] Confirmed from Fjord Foundry official docs (LBP FAQ, Fixed Price Sale FAQ, Tiered Sale creation guide)

- **Manual close (issuer):** Partial.
  - **LBPs:** Cannot be cancelled once started. The creator can **pause swaps** (temporarily halt trading) but cannot end the LBP early or withdraw funds before the scheduled end time. Token weights and pricing parameters cannot be altered mid-sale.
  - **Fixed Price Sales:** Can be cancelled at any time **before** the sale begins. Once started, cannot be cancelled — but trading can be paused and the sale hidden from public view.
  - **Tiered Sales:** Creator has rights to Pause, Unpause, or Cancel the sale before it starts.
- **Automatic close triggers:** Time-based expiry is the primary close trigger. LBPs run for a configured duration (typically 2–5 days) and end automatically. Optional hard cap can be set on LBPs — once reached, no further purchases accepted. Fixed Price Sales close when all tokens are sold (raise limit reached) or time expires.
- **Emergency halt/pause:** Yes — **creator can pause and resume swaps** on LBPs at any time during the sale. This temporarily stops new participation but does not end the sale. The sale can also be hidden from the public interface. This is a creator-only action; Fjord platform team may also have backend controls but this is not documented.
- **Admin override:** Not documented. Fjord's FAQ does not mention platform-level force-close capabilities. Given that LBPs operate on Balancer smart contracts with the creator as pool controller, Fjord may have limited ability to intervene at the contract level. Platform-level actions (hiding sales, UI restrictions) are likely available.
- **Resume after pause:** Yes — pausing swaps is explicitly reversible. The creator can pause and resume swaps during the LBP. This is a toggle, not a permanent halt.
- **Post-close behavior:** Manual claim. After the LBP ends: (1) tokens can be claimed by participants, (2) collateral is sent to the creator's wallet minus the 5% Fjord fee, (3) optional claim delay can be configured to allow time for LP setup before participants receive tokens. Unsold tokens in Fixed Price Sales remain in the project's wallet.
- **Enforcement:** Hybrid — LBP pause/resume is on-chain (Balancer smart pool `setSwapEnabled` function called by pool controller). Sale cancellation and visibility controls are platform-level (Fjord dashboard). Weight schedules are immutable once set on-chain.

> [!analysis] Fjord provides meaningful creator control during sales (pause/resume swaps) without allowing parameter manipulation (weights are locked). This is a good balance — creators can respond to unusual market conditions (e.g., excessive bot activity) without being able to manipulate the price curve. The inability to cancel a live LBP is an important trust property: participants know the sale will complete on schedule.

## Open Questions
- Does Fjord support on-chain KYC/identity proofs for whitelists, or only address-based allowlists?
- What chains beyond Ethereum are live?
- Is whitelist enforced via Merkle proof on-chain or off-chain API?

## Sources
- https://www.fjordfoundry.com/
- https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
- https://medium.com/@fjordfoundry/fjords-upcoming-fjo-token-lbp-and-tge-everything-you-need-to-know-32402218e77e
