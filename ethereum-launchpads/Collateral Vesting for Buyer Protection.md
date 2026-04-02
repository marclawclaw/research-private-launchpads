---
topic: Collateral Vesting for Buyer Protection
type: concept
tags: [vesting, timelock, buyer-protection, rug-pull, collateral, milestone-gating, launchpad, governance]
confidence: medium
last_updated: 2026-04-02
sources:
  - https://ethereum.stackexchange.com/questions/30000/how-to-impose-a-timelock-vesting-for-erc20-tokens-during-icocrowdsale
  - https://phemex.com/academy/crypto-vesting-and-cliffs
  - https://academy.binance.com/en/glossary/token-lockup
---

## Summary
Collateral vesting for buyer protection routes raised funds from a token sale into a vesting/timelock contract rather than releasing them directly to the project creator. This is distinct from standard team token vesting — it protects buyers by ensuring the project team cannot immediately exit with raised capital, and by linking fund release to verifiable milestones or time-based conditions. The pattern is underused in practice; most launchpads release funds to creators at sale close with no delay.

## Key Facts

### What This Pattern Is (and Is Not)

> [!fact] Standard vesting in crypto = team tokens unlock over time (prevents team from dumping). Collateral vesting for buyer protection = raised FUNDS (ETH/USDC) unlock to creator over time (prevents rug pull on capital).

These are different concerns:
- **Team token vesting**: locks the tokens the team received at TGE — prevents insider sell pressure
- **Collateral vesting (buyer protection)**: locks the money the team raised from buyers — prevents the team from taking funds and abandoning the project

The buyer protection pattern is rarely implemented in crypto launchpads despite being standard in traditional crowdfunding (e.g., Kickstarter's escrow model).

### Release Schedule Variants

**1. Linear vesting (time-only)**
- Raised funds released pro-rata over N months
- E.g., 24-month linear: team gets 1/24 of raised capital per month
- Simple to implement; no oracle dependency
- Does not link fund release to actual project progress

**2. Cliff + linear**
- No release for first M months (cliff), then linear over remaining period
- Protects against very early abandonment; commonly used for team compensation
- Same limitation: purely time-based, not progress-based

**3. Milestone-gated release**
- Funds released in tranches upon completion of predefined milestones
- Milestones must be verified by an authority (oracle, governance, multisig)
- Most aligned with buyer interests; most complex to implement

### The Milestone Authority Problem

> [!analysis] Milestone-gated vesting defeats its own purpose if the milestone authority is the same entity as the creator, or if the creator controls the authority. A project team that controls both the vesting contract and the milestone oracle can trigger fund releases at will.

The authority question:
- **Creator-controlled authority** (worst): Team decides their own milestones are met. No protection.
- **Single trusted third-party**: Centralisation risk; requires trust in one entity
- **Multisig (M-of-N)**: Better; requires multiple independent signers to agree
- **DAO/governance vote**: Decentralised but slow; governance can be captured
- **Programmatic oracle**: Hardest to implement; requires objective, on-chain-verifiable milestone metrics

**Critical design requirement**: The cancellation authority and the milestone authority must be **separated from the creator**:
- `cancelAuthority` → should be held by a neutral governance body or multisig (allows clawback of unvested funds to buyers in case of fraud)
- `milestoneAuthority` → should be delegable but explicitly exclude the project creator
- The creator should be a beneficiary only, with no role in approving their own milestones

### How Existing Protocols Handle This

Most existing protocols **do not** implement collateral vesting for buyer protection:
- **Balancer LBP / Fjord Foundry**: Raised collateral returned to creator at sale close — no vesting, no delay
- **DAO Maker DYCO**: Closest to buyer protection — allows refunds if token underperforms post-TGE (performance refund, not pre-release vesting). See [[Refund Mechanisms Comparison]]
- **Regulation CF (US)**: Legally requires an escrow agent to hold funds until a minimum target is met; funds returned to buyers if target missed. This is the regulatory analogue of the pattern.

> [!fact] The closest Web2 analogue is Kickstarter's "all-or-nothing" model: funds held in escrow until project hits its funding goal, then released to creator in a single tranche. No milestone-gated release.

### Cross-Program Call Dependencies

Implementing collateral vesting as a separate contract from the launchpad creates composability dependencies:

```
LaunchpadContract
    ├── calls → VestingContract.deposit(raised_collateral)  [at sale close]
    ├── calls → VestingContract.release(tranche)           [on milestone]
    └── calls → VestingContract.cancel(unvested_amount)    [on governance vote]
```

- The launchpad must lock raised collateral into the vesting contract at sale close in a **single atomic transaction** — if this is two-step, there's a window where the creator could withdraw before vesting is applied
- Cancellation (returning unvested funds to buyers) requires the vesting contract to know the original buyer addresses and amounts — this is a separate data structure from the launchpad's sale records
- On Solana/CosmWasm: cross-program calls are explicit; the launchpad program must have a CPI (cross-program invocation) path to the vesting program
- On EVM: requires a trusted interface between the launchpad contract and the vesting contract; admin key rotation must be considered

### Practical Implementation Sketch

```solidity
// At sale close (called by launchpad):
function lockCollateral(address creator, uint256 amount, MilestoneSchedule schedule) external {
    require(msg.sender == launchpad, "Only launchpad");
    // Route raised funds to vesting contract; creator cannot touch them directly
    vestingSchedules[creator] = VestingSchedule({
        totalAmount: amount,
        released: 0,
        milestones: schedule,
        milestoneAuthority: schedule.governanceAddress, // NOT creator
        cancelAuthority: dao
    });
    emit CollateralLocked(creator, amount);
}

// Milestone approval (NOT callable by creator):
function approveMilestone(address creator, uint256 milestoneIndex) external {
    require(msg.sender == vestingSchedules[creator].milestoneAuthority);
    require(msg.sender != creator, "Creator cannot self-approve");
    // Release tranche to creator
}
```

### Rug Pull Prevention Effectiveness

| Mechanism | Prevents early exit | Linked to progress | On-chain enforcement | Creator cannot bypass |
|---|---|---|---|---|
| Linear vesting (time) | ✅ partial | ❌ | ✅ | ✅ |
| Cliff + linear | ✅ partial | ❌ | ✅ | ✅ |
| Milestone-gated (creator authority) | ✅ nominal | ✅ nominal | ✅ | ❌ (defeats purpose) |
| Milestone-gated (independent authority) | ✅ strong | ✅ | ✅ | ✅ |
| Soft cap + return (Reg CF model) | ✅ (pre-close) | ❌ | depends | depends |

## How it relates to Logos

> [!analysis] This pattern is a direct requirement gap in both RFP-015 (bonding curve) and RFP-016 (LBP). Neither RFP specifies what happens to raised collateral after a successful sale. Without collateral vesting, buyers have no protection against the project team exiting with funds immediately post-launch.

Logos-specific considerations:
- A permissioned launchpad in the Logos ecosystem has an opportunity to implement collateral vesting natively — differentiating from permissionless competitors
- The milestone authority could be delegated to a Logos-native DAO or multi-sig council
- For ZK-private launches, the buyer list for cancellation clawback is hidden — this creates a design challenge: how do anonymous buyers claim refunds from a cancelled vesting schedule?
- Cross-program composability in the Logos environment needs to be explicitly designed — the launchpad and vesting components should be separate programs with well-defined CPI interfaces
- See also: [[Sablier Protocol]], [[Hedgey Finance]], [[Streamflow Finance]] for existing vesting contract primitives

## Open Questions
- How do anonymous buyers (in a ZK-private sale) claim their share of returned collateral if the sale is cancelled?
- Can milestone verification be done programmatically on-chain without a trusted oracle (e.g., verifying on-chain metrics like TVL, DAU, protocol fees earned)?
- Should the milestone authority be a fixed governance address set at sale creation, or configurable post-sale via governance upgrade?
- What is the minimum viable milestone schedule — should it be standardised (e.g., 3 tranches at 3/6/12 months) or fully customisable?
- How does this interact with the LBP "collateral ownership" problem — in a failed LBP, should collateral go back to buyers, and is a vesting contract even relevant for failed sales?

## Sources
- https://ethereum.stackexchange.com/questions/30000/how-to-impose-a-timelock-vesting-for-erc20-tokens-during-icocrowdsale
- https://phemex.com/academy/crypto-vesting-and-cliffs
- https://academy.binance.com/en/glossary/token-lockup
- https://ethereum.stackexchange.com/questions/119432/how-to-implement-a-time-locked-crowd-sale-with-multiple-vesting-schedule-and-tok
