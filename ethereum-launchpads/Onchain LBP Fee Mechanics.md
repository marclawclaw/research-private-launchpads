---
topic: Onchain LBP Fee Mechanics
type: analysis
tags: [fees, onchain, balancer, lbp, weighted-pool, smart-contract]
confidence: high
last_updated: 2026-04-09
sources:
  - https://github.com/balancer/balancer-v2-monorepo/blob/master/pkg/pool-weighted/contracts/lbp/LiquidityBootstrappingPool.sol
  - https://docs.balancer.fi/concepts/explore-available-balancer-pools/weighted-pool/weighted-math.html
  - https://docs.balancer.fi/concepts/vault/swap-fee.html
  - https://docs.balancer.fi/concepts/governance/protocol-fees.html
  - https://docs.balancer.fi/concepts/protocol-fee-model/protocol-fee-model.html
  - https://docs.balancer.fi/concepts/core-concepts/pool-creator-fee.html
  - https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq
---

## Summary

Analysis of how fees are enforced onchain in Balancer weighted pools
and Liquidity Bootstrapping Pools (LBPs), covering both Balancer v2
(production standard for LBPs) and Balancer v3, plus Fjord Foundry's
platform fee layer on top.

## Balancer v2: Swap Fee Mechanics

### Fee application point

The swap fee is deducted from the **input amount before** the weighted
math formula runs. The Balancer v2 documentation states explicitly:
"the pool collects swap fees as a percentage of the input token.
\[The amount used in the formula] is the amount that the pool
actually swaps into the output token, not the amount sent by a
swapper."

> [!fact] Source: [Balancer Weighted Math docs](https://docs.balancer.fi/concepts/explore-available-balancer-pools/weighted-pool/weighted-math.html), accessed 2026-04-09

The adjusted input is computed as:

```
A_in = A_sent × (1 - swap_fee_percentage)
```

This `A_in` is then substituted into the standard weighted pool
out-given-in formula:

```
A_out = B_out × (1 - (B_in / (B_in + A_in)) ^ (W_in / W_out))
```

### LBP contract implementation

In `LiquidityBootstrappingPool.sol`, the `_onSwapMinimal` function
handles fees directly:

```solidity
// For GIVEN_IN (exact input):
request.amount = request.amount.mulDown(
    getSwapFeePercentage().complement()
);
// This computes: amount × (1 - fee), rounding down (higher fee)
```

For exact-out swaps, the inverse applies:

```solidity
return amountIn.divUp(getSwapFeePercentage().complement());
// This computes: amount / (1 - fee), rounding up (higher fee)
```

Both directions round against the trader (in favour of the pool),
matching the standard Balancer rounding convention.

> [!fact] Source: [LiquidityBootstrappingPool.sol](https://github.com/balancer/balancer-v2-monorepo/blob/master/pkg/pool-weighted/contracts/lbp/LiquidityBootstrappingPool.sol), accessed 2026-04-09

### No LBP-specific fee logic

The LBP contract does **not** add any custom fee logic on top of
the standard weighted pool fee handling. Fee deduction in
`_onSwapMinimal` is identical to standard weighted pools. The only
LBP-specific behaviour in the contract is time-dependent weight
interpolation; fee mechanics are inherited unchanged.

### Fee configuration

The swap fee percentage is set by the **pool owner** (the address
that deployed the pool, or the controller contract). In managed
pools and LBPs, the owner can update the swap fee via
`setSwapFeePercentage()`, inherited from the parent settings
contract. The valid range in v2 is **0.0001% to 10%** (1e12 to
1e17 in 18-decimal fixed point).

For Fjord Foundry LBPs, the swap fee is configured at **2%**.

> [!fact] Source: [Fjord LBP FAQ](https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq), accessed 2026-04-09

### Fee destination

The fee portion stays **in the pool** (increasing LP value), minus
the protocol fee share (see below). It is not transferred to a
separate account at swap time.

## Balancer v2: Protocol Fee

The protocol fee is a **percentage of the swap fee**, not of the
total swap amount. The current rate is **50%** of collected swap
fees (set by Balancer governance via BIP-371, August 2023).

Example: if a pool charges a 1% swap fee and the protocol fee is
50%, then 0.5% goes to LPs (stays in pool) and 0.5% goes to the
Balancer `ProtocolFeesCollector` contract.

From the swapper's perspective, the total cost is the same
regardless of the protocol fee split; the protocol fee only affects
how the collected fee is distributed between LPs and the protocol.

> [!fact] Source: [Balancer Protocol Fees docs](https://docs.balancer.fi/concepts/governance/protocol-fees.html), accessed 2026-04-09; [Balancer v2 Fees GitBook](https://balancer.gitbook.io/balancer-v2/concepts/fees)

All protocol fees are accumulated in the `ProtocolFeesCollector`
contract. Balancer governance (DAO multisig) decides how to
distribute them (historically to veBAL holders and DAO treasury).

## Balancer v3: Changes to Fee Model

Balancer v3 made several structural changes to fee handling:

### Swap fee moved to the Vault

In v3, swap fees are managed by the **Vault**, not individual pools.
The Vault stores a `staticSwapFeePercentage` per pool and enforces
it. Pools no longer implement their own fee deduction logic.

> [!fact] Source: [Balancer v3 Swap Fee docs](https://docs.balancer.fi/concepts/vault/swap-fee.html), accessed 2026-04-09

### Fee still charged on input

The fee is still "always charged on the amount in" (on the given
amount for EXACT_IN, on the calculated amount for EXACT_OUT).
The fundamental input-side deduction model is unchanged from v2.

### No Vault-level fee limits

Unlike v2, v3 does not impose Vault-level limits on swap fee
percentages. Instead, limits are set per pool type via the
`ISwapFeePercentageBounds` interface:
- Weighted pools: 0.001% to 10%
- Stable pools: 0.0001% to 10%

### Protocol fee rates

| Fee Type | v2 | v3 |
|----------|----|----|
| Swap fee share | 50% | 50% |
| Yield fee share | 50% | 10% |

Yield fees were reduced to encourage adoption of v3's boosted
pool technology. Swap fee share remains at 50%.

> [!fact] Source: [Balancer v3 Protocol Fee Model](https://docs.balancer.fi/concepts/protocol-fee-model/protocol-fee-model.html), accessed 2026-04-09

### Pool Creator Fee (new in v3)

v3 introduces a **Pool Creator Fee**: pool deployers can earn a
share of swap and yield fees from their pool by specifying a
`poolCreator` address at registration. The creator fee is
calculated net of protocol fees (protocol takes its share first).
Creators claim accrued fees via `withdrawPoolCreatorFees`.

> [!fact] Source: [Balancer Pool Creator Fee docs](https://docs.balancer.fi/concepts/core-concepts/pool-creator-fee.html), accessed 2026-04-09

### Dynamic swap fees via hooks

v3 supports dynamic fee computation through hooks
(`onComputeDynamicSwapFeePercentage`). Pools can implement
volatility-based fees, tiered fees by swap size, or directional
incentives.

### LBP support in v3

LBPs remain a recognised pool type in v3 documentation, using
weighted math with time-dependent weights. The pool owner selects
starting and ending weights and times. Only the pool owner can add
liquidity (before sale start) and remove proceeds (after end time).

## Fjord Foundry: Platform Fee Layer

### The 5% issuer fee

Fjord Foundry charges a **5% fee on collateral raised**, deducted
at sale close. The Fjord LBP FAQ states: "Collateral is sent to
your wallet (minus the 5% Fjord fee)."

> [!fact] Source: [Fjord LBP FAQ](https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq), accessed 2026-04-09

### Enforcement mechanism

The 5% fee is collected when the creator calls the "Close sale"
function. Funds (minus 5%) are then automatically sent to the
creator's wallet. The close function is a required step; funds
cannot be withdrawn during the sale.

> [!fact] Source: [Fjord Token and Liquidity Claiming docs](https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/fjord-features/token-and-liquidity-claiming), accessed 2026-04-09

Fjord's LBP wrapper contract (historically known as the Copper
Launch proxy/LBPManager) acts as the **pool controller** for the
underlying Balancer pool. The creator interacts with Fjord's
contract, not Balancer directly. Because Fjord's contract is the
pool owner, only Fjord's contract can call `exitPool` on Balancer,
allowing it to enforce the 5% deduction before forwarding
proceeds.

> [!analysis] The 5% fee is almost certainly enforced onchain by Fjord's wrapper contract, since the creator cannot call `exitPool` directly (they are not the Balancer pool owner). However, Fjord's LBP contract source code is not publicly available on GitHub (the 2024 Cyfrin audit at github.com/Cyfrin/2024-08-fjord covered staking, auction, token, and points contracts, but not the LBP wrapper). The exact smart contract enforcement cannot be confirmed from public sources.

### Two fee layers in Fjord LBPs

Fjord LBPs have two distinct fee layers, both onchain:

1. **Balancer swap fee (2%)**: deducted from input on every
   swap, enforced by `LiquidityBootstrappingPool.sol`. Split 50/50
   between pool LPs and Balancer protocol.
2. **Fjord platform fee (5%)**: deducted from accumulated collateral
   at sale close, enforced by Fjord's wrapper contract.

The swap fee is per-transaction; the platform fee is at-close.
From the buyer's perspective, only the swap fee affects their
execution price. The 5% platform fee reduces the creator's
proceeds but does not appear in the swap price.

## Relevance to Logos

For the LEZ LBP launchpad (RFP-016), the key design inputs from
this analysis are:

1. **Input-side fee deduction is the proven standard.** Both
   Balancer v2 and v3 deduct fees from the input amount before
   the swap formula. This is well-understood, audited at scale,
   and does not interfere with the weight-shifting mechanism.

2. **Per-swap vs at-close are complementary, not exclusive.**
   Balancer uses per-swap fees (for LPs and protocol); Fjord adds
   an at-close fee (for the platform). Both are enforced onchain
   by different contracts.

3. **At-close fees require the protocol to control the pool exit.**
   Fjord can enforce its 5% because its wrapper contract is the
   pool owner. If the LEZ launchpad wants an at-close fee, the
   program must be the authority that controls withdrawal.

4. **Per-swap fees are simpler for a permissionless system.**
   They require no post-close settlement, work regardless of
   whether the sale completes successfully, and accrue revenue
   immediately. For bonding curves where 98%+ never graduate,
   per-swap is the only viable model.

5. **Balancer v3's Pool Creator Fee is a novel design.** It allows
   pool deployers (analogous to sale creators) to earn a share of
   swap fees. This could be relevant if the LEZ launchpad wants to
   share protocol fee revenue with sale creators.

See also: [[Fee Structure Comparison]], [[Fjord Foundry]], [[Liquidity Bootstrapping Pool (LBP)]]

## Sources

- [Balancer v2 Weighted Math](https://docs.balancer.fi/concepts/explore-available-balancer-pools/weighted-pool/weighted-math.html), accessed 2026-04-09
- [LiquidityBootstrappingPool.sol](https://github.com/balancer/balancer-v2-monorepo/blob/master/pkg/pool-weighted/contracts/lbp/LiquidityBootstrappingPool.sol), accessed 2026-04-09
- [Balancer v3 Swap Fee](https://docs.balancer.fi/concepts/vault/swap-fee.html), accessed 2026-04-09
- [Balancer v2 Protocol Fees](https://docs.balancer.fi/concepts/governance/protocol-fees.html), accessed 2026-04-09
- [Balancer v3 Protocol Fee Model](https://docs.balancer.fi/concepts/protocol-fee-model/protocol-fee-model.html), accessed 2026-04-09
- [Balancer Pool Creator Fee](https://docs.balancer.fi/concepts/core-concepts/pool-creator-fee.html), accessed 2026-04-09
- [Fjord Foundry LBP FAQ](https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/faqs-creators/lbp-faq), accessed 2026-04-09
- [Fjord Token and Liquidity Claiming](https://help.fjordfoundry.com/fjord-foundry-docs/for-sale-creators/fjord-features/token-and-liquidity-claiming), accessed 2026-04-09
- [Cyfrin 2024-08-fjord audit repo](https://github.com/Cyfrin/2024-08-fjord) (staking contracts only, not LBP), accessed 2026-04-09
