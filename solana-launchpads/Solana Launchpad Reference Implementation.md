---
topic: Solana Token Launchpads & Permissioned Sales
type: concept
tags: [solana, launchpad, token-sale, spl, reference-implementation]
confidence: high
last_updated: 2026-03-27
sources:
  - https://github.com/solana-labs/launchpad
  - https://raw.githubusercontent.com/solana-labs/launchpad/master/README.md
---

# Solana Launchpad Reference Implementation

## Summary
The `solana-labs/launchpad` repo is the official Solana Program Library reference for trustless, decentralized token distribution. It locks seller tokens in a program-controlled account and offers them via dynamic pricing models. This is a foundational building block — not a production-ready SaaS product.

## Key Facts
- Part of the Solana Program Library (SPL), Apache 2.0 licensed
- **Core mechanic:** Seller locks tokens into launchpad PDA; buyers purchase at price determined by a pricing model
- **Goals:** maximize funds raised, transparency, seller control
- Uses on-chain program accounts (PDAs) to hold escrowed tokens — fully trustless
- Supports **multiple pricing models** (exact models not documented in README — require source inspection)
- No native whitelist/permissioning in the reference implementation; access control must be layered on top
- Community contributions welcome; repo follows Solana Program Library contribution guidelines

> [!fact] Confirmed from official README and GitHub page
> This is a reference/library implementation, not a deployed production launchpad

## How it relates to Logos
- Demonstrates the pattern for a Logos-native trustless token sale: lock tokens in a program, define pricing, let buyers in
- The absence of native permissioning in this reference means a Logos launchpad would need to add access-control (whitelist, KYC attestations, or ZK gating) as a separate layer
- Pattern: PDA escrow + pricing model + optional permissioning layer = composable launchpad architecture

## Open Questions
- What are the exact pricing models supported? (fixed price, Dutch auction, bonding curve?)
- Is there any audit of this code?
- How does it handle unsold tokens / refunds?
- Is it actively maintained or effectively archived?

## Sources
- https://github.com/solana-labs/launchpad
