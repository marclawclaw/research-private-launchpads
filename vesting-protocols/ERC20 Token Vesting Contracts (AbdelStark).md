---
topic: Token Vesting & Distribution Protocols
type: concept
tags: [ERC20, smart-contracts, open-source, solidity, reference-implementation]
confidence: high
last_updated: 2026-03-27
sources: [https://github.com/AbdelStark/token-vesting-contracts]
---

## Summary
AbdelStark/token-vesting-contracts is a reference open-source implementation of ERC-20 token vesting smart contracts using Solidity. It provides a production-grade `TokenVesting` contract with cliff and linear vesting, optional revocability, Hacken security audit, and dual Hardhat/Forge toolchain support.

## Key Facts
- **Language:** Solidity (ERC-20 compatible)
- **License:** Apache-2.0
- **Toolchains:** Forge (Foundry) + Hardhat — both supported
- **npm package:** `erc20-token-vesting`
- **Audit:** Hacken security audit (report in repo)
- **Features:**
  - Gradual token release (cliff + vesting period)
  - Optionally revocable schedules (owner can cancel)
  - Multiple vesting schedules per beneficiary
  - Supports any ERC-20 token
- **Also known as:** `abdelhamidbakhta/token-vesting-contracts` (original author handle)

## Contract Architecture
- `TokenVesting.sol`: Main contract holding tokens and managing schedules
- Schedule struct: `beneficiary`, `cliff`, `start`, `duration`, `slicePeriodSeconds`, `revocable`, `amountTotal`, `released`, `revoked`
- `createVestingSchedule()` — owner creates schedule for beneficiary
- `release()` — beneficiary triggers token release for vested amount
- `revoke()` — owner can revoke revocable schedules and reclaim unvested tokens
- `computeReleasableAmount()` — view function returning claimable tokens

> [!fact] Confirmed from official docs
> Contract has been audited by Hacken; audit report is available in the repository under /audits/.

## Code Pattern (Cliff + Linear)
```solidity
// After cliff: linear release
uint256 vestedAmount = schedule.amountTotal * timeFromStart / schedule.duration;
```

## How it relates to Logos
- This is the go-to reference implementation for building custom vesting on any EVM-compatible chain Logos may deploy to
- Apache-2.0 license means it can be used/modified freely in Logos ecosystem tooling
- The revocability pattern is important for launchpad use: investors may need clawback mechanisms in case of fraud

## Open Questions
- Is this actively maintained or effectively archived?
- Does it support multi-token (ETH + ERC-20) or only ERC-20?
- Has it been deployed on any major projects? TVL?
- Are there gas optimizations vs. Sablier's implementation?

## Sources
- https://github.com/AbdelStark/token-vesting-contracts
- https://github.com/abdelhamidbakhta/token-vesting-contracts/blob/main/audits/hacken_audit_report.pdf
