---
topic: Allowlist Privacy and K-Anonymity Analysis
type: analysis
tags: [privacy, k-anonymity, allowlist, zk-proofs, set-membership, anonymity-set, logos, lez]
confidence: medium
last_updated: 2026-04-02
sources:
  - https://ideausher.com/blog/privacy-preserving-token-issuance-platform-development/
  - https://obj.umiacs.umd.edu/ieeesp23/zk-creds.pdf
  - https://arxiv.org/html/2603.25190v1
  - https://arxiv.org/pdf/2501.03391
---

## Summary
Using an allowlist in a private token sale creates a privacy tradeoff: an observer who knows the allowlist can narrow down which address made a purchase to the set of allowlisted addresses (k-anonymity set = allowlist size). However, in a ZK-private execution environment like Logos' Execution Zone (LEZ), this framing may be misleading — any private account interaction fits within the whole-chain anonymity set, not just the allowlist. The true privacy analysis depends critically on whether the execution environment is transparent or shielded.

## Key Facts

### K-Anonymity in Allowlists: The Basic Argument

**Definition**: A participant has k-anonymity if their identity is indistinguishable from at least k-1 other users.

**The concern**:
- If an allowlist contains 50 addresses and a purchase is observed on-chain, the observer knows the buyer is 1 of 50
- k-anonymity = 50 (only allowlisted addresses could have bought)
- Compare: if there is no allowlist, k-anonymity = all active wallets on the network (potentially millions)
- A smaller allowlist = smaller anonymity set = weaker privacy

> [!analysis] This argument is valid on transparent chains (Ethereum, Solana) where: (1) the allowlist is public, (2) wallet addresses are pseudonymous but linkable, and (3) transaction contents are observable. In this context, an allowlist of 50 is a significant privacy degradation.

**Example on a transparent chain:**
```
Allowlist = {Alice, Bob, Carol, ... (50 addresses)}
Observer sees: purchase transaction from address X
Observer infers: X ∈ {allowlist of 50}
Privacy = 1/50 (attacker has 2% chance of guessing correctly by random)
vs. no allowlist: 1/1,000,000 (much stronger anonymity)
```

### The Counter-Argument: Private Accounts in LEZ

The key insight from the RFP-015/016 PR discussion (Franck's comment):

> [!analysis] In Logos' Execution Zone (LEZ), the relevant anonymity set is NOT the allowlist — it's all private accounts in the zone. If the allowlist is implemented using **private accounts** (ZK-hidden addresses), an external observer cannot determine who is on the allowlist. Any interaction that looks like "a private account did something" is indistinguishable from any other private account interaction.

This argument has two components:

**1. The allowlist itself can be private**
- If allowlist membership is verified via a ZK set membership proof (not by checking a public address list), the allowlist is not public information
- An observer sees only: "a valid ZK proof was submitted" — they cannot enumerate allowlist members
- The anonymity set becomes: all accounts that *could* have generated a valid ZK set membership proof

**2. LEZ should not be treated as a transparent chain**
- LEZ is a shielded execution environment — private account activity should be private by construction
- An interaction by a private account in LEZ reveals: (1) that *some* private account did *something*, but not who or what
- This is fundamentally different from transparent chain analysis
- The privacy guarantee comes from the zone-wide shielding, not from the anonymity set size of the allowlist

> [!fact] In a fully private execution zone, the anonymity set for any action is bounded by the total number of private accounts in the zone — regardless of allowlist size. The allowlist determines eligibility, not visibility.

### ZK Set Membership Proofs: How They Work

A ZK set membership proof allows a participant to prove "I am a member of this set" without revealing which member they are.

**Standard construction using Merkle trees:**
1. Build a Merkle tree over allowlist entries (hashed identities)
2. Publish only the Merkle root on-chain
3. Participant proves: `I know a leaf L and a path P such that MerkleVerify(root, L, P) = true`
4. The proof reveals nothing about which leaf (which allowlisted identity)

**Additional privacy properties:**
- **Nullifier**: add a one-time-use nullifier to prevent the same allowlist entry from participating twice (Sybil resistance without revealing identity)
- **Rate limiting**: limit each allowlist entry to K purchases without revealing who made which purchase
- **Credential binding**: prove the leaf corresponds to a credential (KYC, token holding) without revealing the credential

> [!fact] ZK set membership proofs (Merkle inclusion proofs under ZK) are standard cryptographic primitives, used in production in Tornado Cash (withdrawal), Semaphore (anonymous signalling), and proposed for privacy-preserving KYC in multiple protocols.

**Libraries/frameworks supporting ZK set membership:**
- **Semaphore** (Ethereum): anonymous group membership signalling
- **Noir** (Aztec): circuits for Merkle membership proofs
- **zk-creds** (academic, IEEE S&P 2023): flexible anonymous credentials from zkSNARKs
- **Penumbra**: account-level privacy inherently provides anonymity set equivalent to all Penumbra users

### The Privacy-Permissioning Tradeoff

| Allowlist Design | Observer can enumerate allowlist? | Observer can link buyer to allowlist entry? | Anonymity set |
|---|---|---|---|
| Public address allowlist (transparent chain) | ✅ Yes | ✅ Yes (via tx origin) | Size of allowlist |
| Public address allowlist (ZK private zone) | ✅ Yes | ❌ No (shielded execution) | All private accounts in zone |
| Private allowlist (ZK set membership) | ❌ No | ❌ No | All accounts that could prove membership |
| No allowlist (transparent chain) | N/A | ✅ Yes (public tx) | All active wallets |
| No allowlist (ZK private zone) | N/A | ❌ No | All private accounts in zone |

> [!analysis] The practical conclusion: in LEZ, *any* allowlist design (public or private) achieves the same privacy level as no allowlist — because the execution zone's shielding prevents linking buyers to allowlist entries. The allowlist only affects *eligibility*, not *privacy*. The k-anonymity criticism is valid for transparent chains but largely inapplicable in a fully shielded execution environment.

### Fair Launch Ideology vs. Permissioned Access

A separate concern (orthogonal to privacy) is whether allowlists are philosophically compatible with "fair launch" principles:

**Arguments against allowlists (even in private zones):**
- Permissioned access creates privileged insiders, regardless of whether the list is private
- The set of allowlisted participants still has an information advantage over non-allowlisted participants
- Fair launch ideology: anyone should be able to participate on equal terms

**Arguments for allowlists:**
- Allowlists enable legal compliance (e.g., restrict to accredited investors for Reg D)
- They enable community-building (whitelist early supporters before launch)
- In practice, "fair" often requires restrictions to prevent Sybil attacks and bot domination
- Without allowlists, frontrunning bots and MEV operators capture most of the value in permissionless launches

**The Logos context:**
- Logos' mission is maximising freedom and individual sovereignty — this leans against arbitrary permissioning
- However, regulatory compliance for token sales in some jurisdictions *requires* some form of permissioning (KYC/accredited investor checks)
- A ZK-proof-based allowlist (prove you pass criteria without revealing identity) may be the Logos-aligned compromise

> [!analysis] The ideal Logos design is a ZK-proof allowlist (not a public address list): prove eligibility (KYC status, token holding, community membership) without revealing identity. This maintains permissioning for compliance while preserving the privacy properties of the shielded zone.

## How it relates to Logos

- For any Logos launchpad using allowlists, the PR discussion's k-anonymity concern should be resolved by using ZK set membership proofs rather than public address lists
- In LEZ, the practical privacy degradation from allowlists is smaller than on transparent chains — the zone's shielding provides protection regardless of allowlist design
- The allowlist concern interacts with [[ZK Token Issuance Patterns]] and [[Aztec Network Overview]]
- The Aztec ($AZTEC) token launch (Nov 2025) used ZKPassport for compliance checks — a production example of privacy-preserving allowlist enforcement

## Open Questions
- What is the minimum allowlist size at which k-anonymity analysis becomes meaningful in practice (even on transparent chains)?
- Can nullifiers prevent double-spending in a ZK set membership allowlist without a centralized nullifier registry?
- How does the anonymity set analysis change if the allowlist uses on-chain credentials (e.g., token holdings) rather than static address lists?
- Should Logos launchpads publish a commitment to allowlist contents (for auditability) or keep it fully private (for maximum privacy)?
- Is there a ZK circuit design that allows: (1) proving allowlist membership, (2) enforcing per-member purchase limits, (3) preventing double-participation — all without revealing identity?

## Sources
- https://ideausher.com/blog/privacy-preserving-token-issuance-platform-development/
- https://obj.umiacs.umd.edu/ieeesp23/zk-creds.pdf (zk-creds: flexible anonymous credentials from zkSNARKs)
- https://arxiv.org/html/2603.25190v1 (zk-X509 Merkle anonymity set analysis)
- https://arxiv.org/pdf/2501.03391 (Privacy-Preserving Smart Contracts, zkSNARK)
- https://protocol.penumbra.zone/main/index.html
