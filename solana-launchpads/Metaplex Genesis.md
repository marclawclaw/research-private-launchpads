---
topic: Metaplex Genesis
type: competitor
tags: [solana, launchpad, tge, fair-launch, permissioned, kyc, allowlist, geo-blocking]
confidence: high
last_updated: 2026-04-02
sources:
  - https://www.metaplex.com/
  - https://developers.metaplex.com/smart-contracts/genesis
  - https://genesis.playsolana.com/
---

## Summary
Metaplex Genesis is a Solana-native smart contract framework for Token Generation Events (TGEs) supporting fair launches (Launch Pools), fixed-price presales, and uniform price auctions. It is the most complete Solana-native launch platform with built-in compliance hooks including KYC gating, wallet allowlists/denylists, and country-specific geo-blocking — all enforced at the smart contract level.

## Key Facts

### Scale & Traction

> [!fact] Confirmed from Metaplex Foundation blog (H1 2025 recap, monthly roundups, CoinMarketCap)
> - **Metaplex total protocol revenue (all products):** >$36M cumulative; $13.7M in H1 2025
> - **Genesis launchpad revenue:** $422K in August 2025 (240% monthly growth); Genesis + TM tokens drove 91-98% of protocol revenue
> - **Total fungible tokens created via Metaplex:** >20 million (Sep 2025)
> - **Unique wallets interacted:** 11.4 million cumulative (3.2M new in H1 2025)
> - **Transaction value:** $2.9B across 121M signed transactions in H1 2025 (29% YoY increase)
> - **Key integrations:** Pump.fun (11.7M tokens), Believe/LaunchCoin, Raydium LaunchLab (258K+ assets), Jup Studio, letsBONK
> - **Genesis status:** Alpha → SDK launched Dec 2025 for third-party integrations

> [!analysis] Genesis itself is still early (most of Metaplex's revenue comes from Token Metadata fees charged to platforms like Pump.fun, not from Genesis launchpad directly). Genesis revenue ($422K/month) is tiny compared to Pump.fun ($45M+/month). However, Genesis is the infrastructure layer — it powers the compliance/permissioning features that Pump.fun lacks.

### Mechanism
- Smart contract program: `GNS1S5J5AspKXgpjz6SvKL66kPaKWAhaGRhCqPRxii2B` (mainnet + devnet)
- Three launch mechanisms: Launch Pool (proportional/fair), Presale (fixed price FCFS), Uniform Price Auction (bid-based)
- Two launch types: Project (full control) and Memecoin (streamlined defaults — 1hr deposit, 50% allocation, 98% Raydium LP)
- No-code UI at genesis.playsolana.com + TypeScript SDK for developers
- Protocol fee: 2% on deposits/withdrawals; no upfront costs
- Bucket system: modular inflow (SOL collection) and outflow (treasury/vesting) components
- Backed by Metaplex Foundation — the dominant NFT/token standard infrastructure on Solana
- On-chain token creation with metadata, fund collection, and distribution in a single coordinated flow

## Allowlist & Access Control

> [!fact] Confirmed from Metaplex Genesis marketing site (genesis.playsolana.com) and developer docs

- **Gating method:** Wallet allowlist/denylist + optional KYC gating + country-specific geo-blocking. Configurable per-launch — can be fully open or fully permissioned
- **Enforcement:** On-chain (smart contract level). Genesis enforces access control directly in the Solana program:
  - **Wallet allowlist:** Only specified wallet addresses can participate in deposits. Enforced at the program instruction level — non-whitelisted wallets cannot call deposit instructions
  - **Wallet denylist:** Specific wallets can be blocked from participation (complement to allowlist)
  - **KYC gating:** Integration with KYC providers to gate participation — only wallets that have completed KYC verification can interact with the launch
  - **Geo-blocking:** Country-specific restrictions enforced at the launch configuration level
  - All enforcement is on-chain and transparent — participants can verify the rules before depositing
- **Tiered access:** Partially — the bucket system allows multiple inflow buckets with different configurations:
  - Different presale tiers can have different prices and allocation caps
  - Launch Pools are inherently egalitarian (proportional distribution to all depositors)
  - Per-wallet minimum and maximum deposit limits configurable
  - No platform-wide tier system (unlike DAO Maker) — tiers are per-launch configuration
- **Geo-blocking:** Yes — built into the smart contract layer. Issuers specify restricted countries during launch configuration. This is one of the few platforms where geo-blocking is enforced on-chain rather than just at the UI level
- **Phased rounds:** Yes — Genesis supports multiple inflow buckets per launch, enabling:
  - Private/seed round (allowlisted wallets, fixed price) → Public round (open, fair launch pool)
  - Deposit windows and claim windows are independently configurable per bucket
  - Time conditions control when actions are allowed (deposit window, claim window)
- **Sybil resistance:** Medium — depends on configuration:
  - With KYC gating: strong (identity-level verification)
  - With allowlist only: moderate (depends on curation quality of the list)
  - With open launch: weak (any wallet can participate, limited by per-wallet caps)
  - Launch Pool mechanism provides natural Sybil resistance: since distribution is proportional, splitting across wallets doesn't increase total allocation
  - Memecoin launch type has no permissioning (fully open 1-hour deposit)

> [!analysis] Metaplex Genesis is the most comprehensive Solana-native solution for permissioned token launches. The on-chain enforcement of allowlists, denylists, and geo-blocking sets it apart from Ethereum platforms where these are typically enforced off-chain at the UI layer. The Launch Pool's proportional distribution is inherently Sybil-resistant (splitting wallets doesn't help if allocation is proportional). However, the KYC integration details are sparse — it's unclear whether this uses Merkle proofs, on-chain attestations, or a centralised oracle model. For Logos, Genesis demonstrates that on-chain compliance enforcement is viable on a high-performance chain — Solana's low fees make per-transaction compliance checks economically feasible.

See also: [[Off-Chain Whitelist Pattern (Merkle Proof)]], [[Solana Launchpad Ecosystem Overview]]

## How it relates to Logos
- Genesis is the closest Solana reference to a "compliant on-chain launchpad" — directly relevant as a design reference for Logos-based token launches
- On-chain geo-blocking enforcement is a novel feature; Logos could implement this with ZK proofs (prove you're NOT in a restricted country without revealing your country)
- The Launch Pool mechanism (proportional distribution) aligns with fairness goals; could be enhanced with privacy (hide individual deposit amounts using ZK)
- Bucket system modularity is a good architectural pattern for composable launch configurations

## Fee Structure

> [!fact] Confirmed from Metaplex developer docs and Genesis marketing site

- **Platform fee (issuer):** 2% protocol fee on deposits — applied automatically by the smart contract on all SOL deposited into Launch Pools, Presales, and Uniform Price Auctions. No upfront cost to create a launch
- **Participant fee (buyer):** The 2% fee is deducted from participant deposits (not from the project's token allocation). Participants effectively pay 2% more than the base token price
- **Listing/setup fee:** None — no-code UI (genesis.playsolana.com) is free to use. TypeScript SDK for custom integrations is open-source
- **Staking requirement:** None — no native token required for participation. Access control is configurable per-launch (open, allowlist, KYC-gated)
- **Gas/proof costs:** Solana network fees (~$0.01-0.02 per transaction) — negligible compared to Ethereum. Borne by participants for deposits and claims
- **Revenue model:** Protocol fee (2% on deposits) is the sole documented revenue source. Backed by Metaplex Foundation (which also earns from NFT minting fees across the broader Metaplex ecosystem)

> [!analysis] Metaplex Genesis has the lowest and most transparent fee structure of any full-featured launchpad — 2% on deposits with zero upfront costs. Compare this to Fjord's 5%, DAO Maker's 5%+, or Securitize's enterprise pricing. The fee is borne by participants (not issuers), making it the cheapest option for projects. Solana's near-zero gas costs amplify the advantage. The tradeoff is that Genesis is Solana-only and relatively new — less battle-tested than established Ethereum launchpads.

## Sale Lifecycle & Close Mechanics

> [!analysis] Metaplex Genesis documentation focuses on setup and participation flows; close/pause mechanics inferred from the bucket/time-condition architecture and developer docs

- **Manual close (issuer):** Limited evidence. Genesis uses **time conditions** (deposit windows and claim windows) that are configured at launch creation. The deposit window defines when users can deposit SOL; once this window closes, no new deposits are accepted. There is no documented "early close" function that allows the issuer to end the deposit window before its scheduled end time. However, the **withdraw** function exists — participants can withdraw deposits during the deposit window (subject to 2% fee), and after launch completion, the creator withdraws raised funds.
- **Automatic close triggers:** Time-based: (1) **Deposit window closes** — no more deposits accepted after the configured end time. (2) **Claim window opens** — participants can claim tokens after the configured start time. For memecoin launches, the deposit window is hardcoded to 1 hour. For project launches, deposit window duration is configurable (48h default). No documented hardcap trigger that closes the deposit window early (Launch Pool is proportional, so more deposits = higher implied price, no cap needed). Presale may have a cap based on available token supply.
- **Emergency halt/pause:** Not documented. Genesis is a permissionless smart contract program — there's no documented pause function or emergency halt mechanism in the public-facing docs. The program authority (Metaplex Foundation) may have upgrade authority over the program, which could theoretically be used to halt operations, but this is not documented as a feature. Individual launches do not appear to have issuer-controlled pause functionality.
- **Admin override:** Limited. Genesis is a Solana program (smart contract) — the program itself is controlled by Metaplex Foundation. Individual launches are controlled by the creator's wallet. There's no documented mechanism for the protocol to force-close or override individual launches. The recommendation to **revoke mint and freeze authorities** post-launch suggests the creator has these authorities initially and can choose to retain them.
- **Resume after pause:** Not applicable — no documented pause mechanism.
- **Post-close behavior:** Automated on-chain:
  - **Launch Pool:** After deposit window closes, token price is discovered (total SOL / total tokens allocated). Participants claim tokens proportional to their deposit share during the claim window. Creator withdraws raised SOL.
  - **Presale:** Tokens distributed immediately on deposit (FCFS). Creator claims raised SOL after deposit window closes.
  - **Memecoin launches:** 50% of tokens go to depositors (proportional), 98% of raised SOL goes to Raydium LP (permanently locked), 1% to creator (unlocked).
  - Post-launch: creators are recommended to revoke mint and freeze authorities for trust.
- **Enforcement:** On-chain (Solana smart contract). All deposit windows, claim windows, and distribution mechanics are enforced by the Genesis program on-chain. Time conditions are immutable once the launch is created. The 2% protocol fee is enforced automatically.

> [!analysis] Metaplex Genesis takes a "set and forget" approach — launch parameters (including timing) are configured at creation and enforced immutably on-chain. This is the most trustless model among the platforms studied: no party (including the creator or Metaplex) can alter the launch parameters after creation. The tradeoff is inflexibility — if something goes wrong (e.g., a vulnerability is discovered mid-launch), there's no emergency brake. The recommendation to revoke authorities post-launch further emphasizes the protocol's trust-minimization philosophy.

## Open Questions
- How does Genesis's KYC gating work technically — Merkle proof, on-chain oracle, or platform-mediated?
- Is the allowlist stored on-chain (account data) or verified via Merkle proofs?
- Can Genesis be combined with Token-2022 extensions (confidential transfers, transfer hooks)?
- What's the maximum allowlist size supported on-chain given Solana account size limits?

## Sources
- https://www.metaplex.com/
- https://developers.metaplex.com/smart-contracts/genesis
- https://genesis.playsolana.com/
