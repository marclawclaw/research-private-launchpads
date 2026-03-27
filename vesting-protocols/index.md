# Token Vesting & Distribution Protocols — Index

Research on token vesting mechanisms, streaming protocols, and distribution tooling for blockchain projects.

## Notes

| File | Type | Summary |
|------|------|---------|
| [[Token Vesting Fundamentals]] | concept | Core concepts: what vesting is, schedule types (linear/cliff/milestone), on-chain vs off-chain, stakeholder groups |
| [[Sablier Protocol]] | competitor | Leading EVM+Solana streaming protocol (est. 2019). Per-second vesting, 27 chains, NFT-based stream ownership, a16z-backed |
| [[Streamflow Finance]] | competitor | Solana-native vesting/distribution platform. Low fees, batch CSV, airdrops, staking, payroll. STREAM token. |
| [[LlamaPay]] | competitor | Multi-chain EVM payroll streaming. 3–4x cheaper than alternatives. Same contract address across all chains. Focus: recurring payments, not vesting |
| [[Team Finance]] | competitor | EVM vesting + LP token locks for early-stage projects. Branded embeddable vesting widget. Multi-chain (BSC, ETH, AVAX, Polygon) |
| [[ERC20 Token Vesting Contracts (AbdelStark)]] | concept | Open-source reference implementation: cliff + linear vesting, revocable schedules, Hacken audit, Apache-2.0 |
| [[Token Streaming vs Discrete Unlocks]] | concept | Design pattern comparison: streaming (per-second) vs discrete unlocks (cliff + periodic). Trade-offs in market impact, UX, complexity |

## Key Themes
- **Streaming** (Sablier, LlamaPay, Streamflow) is replacing discrete unlocks as the dominant model
- **Security audits** are table stakes — every production protocol has been audited
- **Gas efficiency** matters: LlamaPay's shared-contract model is 3–4x cheaper than per-stream deployments
- **Multi-chain** deployment with consistent addresses is an emerging standard (LlamaPay pattern)
- **NFT-based stream ownership** (Sablier) enables secondary market for vesting positions

## Relevance to Logos Launchpad
- A Logos launchpad needs at minimum: cliff + linear vesting + revocability
- Streaming model is the UX upgrade worth implementing for competitive differentiation
- Privacy-preserving vesting (hidden amounts, ZK-proven compliance) is a Logos-native opportunity not covered by any existing protocol
- See also: [[../kyc-compliance/index]] for compliance requirements around token distributions
