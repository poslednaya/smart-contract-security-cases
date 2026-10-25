# EVM Smart Contract Security Case Studies

Curated technical notes on **publicly disclosed EVM/Solidity vulnerabilities**. The focus is on state transitions, accounting invariants, precision and rounding, access control, and formal-verification research.

> **Attribution:** These are third-party findings described in their original public reports, **not my own audit discoveries**. Suggested invariants are research ideas, not properties proven by `pevm`. Original PoCs have not been independently executed for this collection.

## Projects

| Date | Protocol | Category | Selected findings | Original report |
| --- | --- | --- | --- | --- |
| Sep 2026 | [Metric OMM](case-studies/2026-07-metric-omm/README.md) | Oracle-based DEX / AMM | 5 Medium | [Sherlock](https://audits.sherlock.xyz/contests/1279) |
| May 2026 | [Olas](case-studies/2026-05-olas/README.md) | Oracle / Protocol-owned Liquidity | 3 High | [Code4rena](https://code4rena.com/reports/2026-01-olas) |
| Apr 2026 | [SukukFi](case-studies/2026-04-sukukfi/README.md) | Async Vault / ERC-7575 | 1 High / 2 Medium | [Code4rena](https://code4rena.com/reports/2025-11-sukukfi) |
| Apr 2026 | [Intuition](case-studies/2026-04-intuition/README.md) | Account Abstraction / Emissions | 2 Medium | [Code4rena](https://code4rena.com/reports/2026-03-intuition) |
| Mar 2026 | [Recall](case-studies/2026-03-recall/README.md) | Cross-chain / IPC (Solidity) | 3 High | [Code4rena](https://code4rena.com/reports/2025-02-recall) |
| Mar 2026 | [Panoptic: Next Core](case-studies/2026-03-panoptic-next-core/README.md) | Options / Lending | 3 High | [Code4rena](https://code4rena.com/reports/2025-12-panoptic-next-core) |
| Feb 2026 | [GTE Spot CLOB and Router](case-studies/2026-02-gte-clob/README.md) | Spot DEX / Order Book | 3 High | [Code4rena](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router) |
| Feb 2026 | [Garden](case-studies/2026-02-garden/README.md) | HTLC / Bridge (Solidity finding) | 1 Medium | [Code4rena](https://code4rena.com/reports/2025-11-garden) |
| Feb 2026 | [Brix Money](case-studies/2026-02-brix-money/README.md) | Cross-chain Staking / Vault | 3 Medium | [Code4rena](https://code4rena.com/reports/2025-11-brix-money) |
| Jan-Feb 2026 | [Fluid DEX v2](case-studies/2026-01-fluid-dex-v2/README.md) | DEX / Lending | 1 case | [Sherlock](https://audits.sherlock.xyz/contests/1225) |
| Dec 2025 | [Monolith Stablecoin Factory](case-studies/2025-12-monolith-stablecoin/README.md) | Stablecoin / Lending | 4 cases | [Sherlock](https://audits.sherlock.xyz/contests/1212) |
| Nov 2025 | [stNXM by EaseDeFi](case-studies/2025-11-stnxm-easedefi/README.md) | Liquid Staking / Oracle | 1 case | [Sherlock](https://audits.sherlock.xyz/contests/1203) |
| Nov 2025 | [Inverse Finance - Junior Tranche](case-studies/2025-11-inverse-junior-tranche/README.md) | Lending / ERC-4626 | 2 cases | [Sherlock](https://audits.sherlock.xyz/contests/1202) |
| Oct-Nov 2025 | [Centrifuge Protocol V3.1](case-studies/2025-11-centrifuge-v3-1/README.md) | RWA / Cross-chain | 3 cases | [Sherlock](https://audits.sherlock.xyz/contests/1028) |
| Oct 2025 | [Index Fun Order Book](case-studies/2025-10-index-fun-order-book/README.md) | Order Book / Prediction Markets | 3 cases | [Sherlock](https://audits.sherlock.xyz/contests/1197) |

**Collection:** 15 EVM projects / 40 selected technical case studies. Each project links to issue-by-issue explanations and its original audit source.

**Scope:** Only EVM/Solidity case studies are retained. The source audit for some projects may also cover non-EVM components; their selected findings here concern Solidity contracts. The Monad client audit is not included because the selected issues involve Rust/C++ client implementation, even though Monad is EVM-compatible.

**Date convention:** Code4rena dates are final-report publication months; Sherlock dates are approximate engagement months except Metric OMM, which is labeled with its final-report publication month.

**Source quality:** Code4rena cases are based on final public reports. Sherlock cases have mixed primary/secondary source coverage; check each project page. Severity labels reflect the supplied report or source and are not independent exploit validations.

## Methodology

For each published finding, the notes identify:

1. Reported root cause and affected functionality.
2. Preconditions and impact, where supported by the source.
3. Possible mitigation / audit direction.
4. Candidate invariants for future formal checking, explicitly not verified.
5. Links back to original findings or reports.

[Case-study template](templates/case-study-template.md) | [Research sources](SOURCES.md) | [Compact profile table](PROFILE_SNIPPET.md) | [Full profile table](PROFILE_SNIPPET_FULL.md)
