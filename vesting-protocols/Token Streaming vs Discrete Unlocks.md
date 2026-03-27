---
topic: Token Vesting & Distribution Protocols
type: concept
tags: [streaming, vesting, design-pattern, tokenomics, UX]
confidence: high
last_updated: 2026-03-27
sources: [https://sablier.com/, https://llamapay.io/, https://streamflow.finance/blog/token-vesting-the-definitive-guide]
---

## Summary
Two dominant paradigms exist for token distribution: discrete unlocks (tokens released at specific dates/milestones) and continuous streaming (tokens accrue per second and are withdrawable at any time). Streaming offers superior UX and reduces speculative volatility around unlock dates; discrete unlocks are simpler to explain and implement.

## Key Facts

### Discrete Unlocks
- Tokens release at specific dates or after milestones
- Creates predictable "unlock events" — known sell pressure dates
- Traditional model (cliff + quarterly/monthly unlocks)
- Used by most early ICOs, IEOs, and launchpads
- Simpler to implement and audit

### Continuous Streaming
- Tokens accrue every second (or block)
- Recipients can withdraw any accrued amount at any time
- No discrete unlock events — sell pressure is smoothed
- Sablier and LlamaPay pioneered this model
- Higher technical complexity but better market stability

## Comparison Table
| Dimension | Discrete Unlocks | Continuous Streaming |
|-----------|-----------------|---------------------|
| Market impact | Concentrated sell events | Diffuse, continuous |
| Recipient UX | Wait for unlock date | Access accrued funds anytime |
| Sender certainty | Predictable dates | Same total, different access |
| Complexity | Low | Medium-High |
| Gas cost | Per-unlock transaction | Withdraw on demand |
| Cliff support | Yes | Yes (stream starts after cliff) |
| Examples | TGE + 3-month cliff + monthly | Sablier, LlamaPay, Streamflow |

> [!analysis] Analyst inference — not verified
> Streaming reduces the "unlock dump" phenomenon common with discrete unlocks. However, it requires token holders to actively manage when to sell, which may disadvantage less-sophisticated holders.

## How it relates to Logos
- A Logos launchpad should support both models — different investor types prefer different paradigms
- Privacy-preserving streaming could be a novel Logos feature: hide streaming amounts from public view while proving compliance
- The streaming model pairs well with [[Sablier Protocol]] NFT ownership — transferable streaming positions

## Open Questions
- Is there empirical data comparing price impact of streaming vs. discrete unlock projects?
- Can streaming and discrete unlocks be combined in the same vesting contract?
- How do tax authorities treat continuously streamed tokens vs. discrete unlock events?

## Sources
- https://sablier.com/
- https://llamapay.io/
- https://streamflow.finance/blog/token-vesting-the-definitive-guide
