---
topic: Liquidity Bootstrapping Pool (LBP)
type: concept
tags: [ethereum, lbp, price-discovery, token-sale, balancer]
confidence: high
last_updated: 2026-04-02
sources:
  - https://balancer.gitbook.io/balancer/smart-contracts/smart-pools/liquidity-bootstrapping-faq
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
---

## Summary
A Liquidity Bootstrapping Pool (LBP) is a dynamic AMM-based token sale mechanism originally developed on Balancer. Pool weights shift over time (typically from token-heavy to collateral-heavy), causing price to decline unless demand keeps buying pressure up. This enables fair price discovery and discourages bots.

## Key Facts
- Originated from Balancer smart pools (v1 docs now deprecated, v2 maintained at docs.balancer.fi)
- Mechanics: two-asset pool (project token + collateral, usually USDC or WETH) with shifting weights
- Starting weights typically 99/1 (token/collateral) → ending 1/99; starting price set ~6–10× fair value
- `updateWeightsGradually` triggers the weight shift; `pokeWeights` (public function) advances it on schedule
- Price naturally falls if no buying; buying pushes price up temporarily
- Arbitrageurs are incentivized to correct mispricing — creates organic price discovery
- Anti-bot property: early sniping is discouraged because price starts high and falls
- Duration: Balancer recommends minimum 3 days (default minimum ~2 weeks in smart pool code)
- Sale creator recovers: remaining tokens + collateral raised (minus fees) by calling `removeToken` or removing liquidity
- Optional: pause swaps, delayed start, max 10% swap fee to discourage front-running at launch
- Platforms implementing LBPs: [[Fjord Foundry]], Copper (merged into Fjord), Balancer directly

## How it relates to Logos
- LBPs provide a trust-minimised price discovery mechanism requiring no pre-set valuation — useful for Logos projects at early token launch stage
- The shift from permissioned VC rounds to open LBP launches aligns with Logos' decentralisation ethos
- Weight-based pricing is a smart contract primitive that could be adapted for permissioned Logos token sales

> [!fact] LBP is a well-established mechanism with many successful launches (Autonolas raised $550k from $50k initial liquidity; others raised $3M+)

> [!analysis] LBPs are fundamentally open/permissionless by design; adding permissioning (whitelist) is a layer on top, not native to the mechanism

## Refund & Participant Protection

> [!fact] LBP mechanics confirmed from Balancer v1/v2 docs and CoinMarketCap glossary

- **Refund window:** No. LBP trades are AMM swaps — irreversible once confirmed on-chain. There is no refund mechanism built into the Balancer smart pool contracts.
- **Minimum raise threshold (soft cap):** No. LBPs have no minimum capital threshold. The pool runs regardless of participation level; low demand simply results in the price falling toward the floor.
- **Post-launch performance refund:** No. Tokens purchased in an LBP are standard ERC-20 holdings with no built-in refund rights.
- **Cancellation rights:** During-sale only. If the LBP is configured for buy+sell mode, participants can sell tokens back into the pool at current AMM price (not purchase price). Pool creators can pause swaps, but this is a creator tool, not buyer protection.

> [!analysis] LBPs provide *structural* buyer protection through their pricing mechanism rather than explicit refund rights:
> 1. **Declining price curve** — price starts high and falls, so rational buyers wait for fair value rather than overpaying
> 2. **Anti-bot design** — high starting price + gradual decline makes sniping unprofitable
> 3. **Price transparency** — all pricing is on-chain and deterministic based on weight schedule
> 4. **Rug-pull resistance** — pool parameters are set at creation and weight changes follow a pre-committed schedule
>
> However, none of these provide a *right to refund* after purchase. A buyer who overpays has no recourse other than selling back at market price.

## Allowlist & Access Control

> [!fact] LBP mechanism confirmed as inherently permissionless from Balancer and Fjord docs

- **Gating method:** Open by default — LBPs are permissionless AMM pools. Any wallet can interact with the smart contract. Permissioning is an optional overlay, not native to the mechanism
- **Enforcement:** On-chain (smart contract level) — LBP pool contracts on Balancer do not include native allowlist logic. Platforms like [[Fjord Foundry]] add off-chain whitelist gating at the UI/platform layer. Custom implementations could add Merkle proof checks or access control modifiers to the pool interaction functions
- **Tiered access:** No — LBPs have no native concept of tiers or allocation sizes. All participants interact with the same AMM pool at market price. Per-wallet limits are not built into standard LBP contracts (Fjord adds this for tiered fixed-price sales, not for LBPs)
- **Geo-blocking:** Not at protocol level. Platform implementations (Fjord, Copper) may add UI-level geo-blocking. The underlying smart contracts are permissionless
- **Phased rounds:** Single phase — LBPs run as a continuous sale with declining price curve. No whitelist-then-public structure. The weight shift schedule creates an implicit time-gating: early buyers pay more, patient buyers get better prices
- **Sybil resistance:** None at protocol level. LBPs are designed for open participation. Anti-bot properties come from the pricing mechanism (high starting price deters sniping), not from identity or stake requirements. Front-running is mitigated by optional swap fees (up to 10%) and high initial price

> [!analysis] The LBP's access control philosophy is deliberately minimal — the mechanism's strength is fair price discovery through open markets, not restricted access. Adding permissioning (whitelists, KYC) to an LBP is conceptually in tension with the open-access ethos but practically necessary for compliance. The design space for "permissioned LBP" (e.g., Merkle-gated pool interactions, ZK-proof KYC checks before swap) is under-explored and represents an opportunity for privacy-preserving fair price discovery in regulated contexts.

See also: [[Token Sale Permissioning Mechanisms]], [[Fjord Foundry]]

## Fee Structure

> [!fact] Confirmed from Balancer v2/v3 docs, Balancer governance documentation, and LBP FAQ

- **Platform fee (Balancer protocol):** Balancer takes 50% of swap fees collected by pools (protocol fee = percentage of swap fees, not of trade volume). E.g., if a pool charges 2% swap fee, Balancer takes 1% of that, not of the trade amount
- **Swap fee (configurable by pool creator):** 0.01% to 10%, set at pool creation. LBP creators typically set 1-5% initially, sometimes starting high (4-5%) to discourage early sniping and reducing over time. V3 has no Vault-level limits on swap fee percentage
- **Pool creation fee:** No explicit pool creation fee. Gas costs for deploying the smart pool contract (~$50-200 on Ethereum mainnet depending on gas prices)
- **Participant fee (buyer):** Swap fee only (set by pool creator, see above). No additional platform-level buyer fee
- **Pool creator fee (V3):** V3 introduces an optional pool creator swap fee and yield fee (both start at 0%, can be set later by pool creator). This allows LBP creators to extract additional revenue
- **Listing/setup fee:** None — permissionless pool creation. Anyone can create an LBP via Balancer directly (requires smart contract interaction) or via Fjord Foundry (which adds its own 5% fee)
- **Staking requirement:** None — fully permissionless
- **Gas/proof costs:** Ethereum gas fees for pool creation, swaps, weight updates (`pokeWeights`), and liquidity removal. Can be $50-500+ per transaction on Ethereum mainnet. L2 deployments significantly reduce costs
- **Revenue model:** Balancer protocol earns from 50% share of all swap fees across all pools. $BAL token governance controls fee parameters. Yield fees (50%) on yield-bearing assets in boosted pools (V3)

> [!analysis] LBP costs are highly variable — the total cost to a project is swap fee configuration (their choice) + gas costs (network-dependent) + Balancer's protocol cut (50% of swap fees). Using Fjord Foundry adds a 5% flat fee on collateral but provides a no-code UI and marketing. Direct Balancer LBP deployment is cheaper but requires technical sophistication. On Ethereum mainnet, gas costs for the full LBP lifecycle (create pool → weight shifts → remove liquidity) can easily exceed $1,000, making L2 deployment increasingly attractive.

## Open Questions
- Can LBPs be combined with ZK-proof identity gating (e.g., prove KYC without revealing address)?
- How does Fjord's "zero liquidity LBP" work at the smart contract level vs. classic Balancer LBP?

## Sources
- https://balancer.gitbook.io/balancer/smart-contracts/smart-pools/liquidity-bootstrapping-faq
- https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
