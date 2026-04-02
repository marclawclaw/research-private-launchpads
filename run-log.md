
## [2026-04-02 14:10] RFP-015/016 PR Gap Analysis — ok
- Notes written: 5 new notes, 1 updated (LBP), 1 index updated
- Sources crawled: github.com/flayerlabs/flaunchgg-contracts, bankless.com/flaunch, blockworks.co/uniswap-v4, github.com/Uniswap/v2-periphery (UniswapV2Library.sol), medium.com/gnosis-auction, docs.molecule.to/bio.xyz, protocol.penumbra.zone, arxiv.org/pdf/2301.13785, ideausher.com/zk-allowlist, obj.umiacs.umd.edu/zk-creds, aztec.network/ticker
- New notes:
  - ethereum-launchpads/Flaunch (Uniswap V4 Hooks Launchpad).md — hook-based bonding curve, fair launch, Progressive Bid Wall, fee routing
  - ethereum-launchpads/Bonding Curve Rounding and Integer Arithmetic.md — V2/V3/V4 rounding direction, pool solvency, graduation implications
  - ethereum-launchpads/Collateral Vesting for Buyer Protection.md — buyer-protection vesting pattern, milestone authority design, cross-program composability
  - ethereum-launchpads/Batch Auctions and Commit-Reveal Token Sales.md — Gnosis Auction, commit-reveal, Penumbra sealed-bid, comparison vs bonding curves
  - zk-privacy-issuance/Allowlist Privacy and K-Anonymity Analysis.md — k-anonymity in allowlists, LEZ counter-argument, ZK set membership proofs
- Updated: LBP note with weight interpolation formula, spot price formula, timestamp dependency, lazy vs poke computation, collateral ownership problem
- Key finding: RFP-015/016 PR surfaced 6 significant design gaps not in prior research. The most critical: (1) hook-based bonding curves are production-ready (Flaunch), (2) LBP collateral at close belongs to buyers not creator, (3) batch auctions are stronger anti-frontrun mechanisms than bonding curves, (4) collateral vesting for buyer protection is an unexplored design space.

## [2026-03-28 06:15] Token Vesting & Distribution Protocols — ok
- Notes written: 7
- Sources crawled: streamflow.finance/blog/token-vesting-the-definitive-guide, sablier.com, github.com/sablier-labs/evm-monorepo, llamapay.io, github.com/AbdelStark/token-vesting-contracts, team.finance/vesting, blog.team.finance
- Key finding: Streaming protocols (Sablier, LlamaPay, Streamflow) are replacing discrete unlocks. Sablier is the EVM gold standard (27 chains, a16z-backed, NFT stream ownership). No protocol offers privacy-preserving vesting — strong Logos opportunity. LlamaPay's shared-contract gas model (3–4x cheaper) is a key design lesson.

## [2026-03-28 03:15] KYC-Gated / Accredited Investor Token Sales & Compliance — ok
- Notes written: 5
- Sources crawled: qubit.capital/blog/token-sales-regulations, sumsub.com/blog/kyc-legal-for-sto, sec.gov/cf-crypto-securities-041025, republic.com/token-dpa, build.avax.network/integrations/securitize, chainalysis.com/erc-3643, erc3643.org, docs.erc3643.org, crowdfundinsider.com (Republic 2025 update), bny.com (Securitize CLO launch)
- Key finding: ERC-3643 is the dominant on-chain KYC enforcement standard; Securitize demonstrated institutional-grade compliance with BlackRock BUIDL. Privacy gap: no ZK-based accredited investor proof exists — strong Logos opportunity.

## [2026-03-28 00:15] ZK Privacy-Preserving Token Issuance — ok
- Notes written: 7
- Sources crawled: aztec.network/basics, aztec.network/blog (governance + security + aztec.nr posts), github.com/AztecProtocol/aztec-packages, penumbra.zone, protocol.penumbra.zone, github.com/penumbra-zone/penumbra, cache256.com/shielded-pools-analysis, penumbra.zone/blog/shielded-staking, bankless.com/aztec-primetime, web search supplemental
- Key finding: No production private launchpad exists on either Aztec or Penumbra — clear build opportunity. Penumbra's sealed-bid ZSwap auction is the best existing anti-frontrun distribution mechanism. Aztec is the right architecture for a programmable compliance-compatible launchpad but remains Alpha-stage (~1 TPS). Both support selective disclosure for compliance.

## [2026-03-27 07:30] Solana Token Launchpads & Permissioned Sales — ok
- Notes written: 5
- Sources crawled: github.com/solana-labs/launchpad, github.com/palsp/solana-launchpad, streamflow.finance, streamflow.finance/blog/token-vesting-definitive-guide, solanacompass.com/launchpads, web search supplemental
- Key finding: No dominant permissioned/private launchpad on Solana. Merkle proof whitelist is the standard primitive. Streamflow is the mature vesting layer. Pump.fun dominates permissionless. Gap exists for institutional KYC+privacy-preserving launchpad.

## [2026-03-27 04:20] Ethereum Private/Permissioned Launchpads — ok
- Notes written: 6
- Sources crawled: fjordfoundry.com, help.fjordfoundry.com/lbp-faq, balancer.gitbook.io/lbp-faq, daomaker.com, polkastarter.com, 99bitcoins.com/ethereum-launchpads, coinmarketcap.com/dao-maker, blog.polkastarter.com, web search supplemental
- Key finding: Clear gap between current staking/KYC permissioning and privacy-preserving ZK-based access — potential Logos product opportunity
