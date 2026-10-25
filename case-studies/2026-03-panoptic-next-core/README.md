# Panoptic: Next Core

**Original engagement:** [Code4rena final findings and analysis](https://code4rena.com/reports/2025-12-panoptic-next-core)  
**Published:** Mar 2026  
**Platform / stack:** EVM / Solidity  
**Focus:** Options / Lending  
**Total findings in report:** 3 High, 19 Medium  
**Selected studies here:** 3

## Selected findings

| Finding | Technical issue | Final severity |
| --- | --- | --- |
| H-01 | [BuilderWallet can be re-initialized and seized](h-01-reinitializable-builderwallet.md) | High |
| H-02 | [Liquidation reentrancy turns phantom shares into real shares](h-02-cross-tracker-phantom-reentrancy.md) | High |
| H-03 | [Commission fee is bypassed in option burn settlement](h-03-commission-fee-bypass.md) | High |

## Notes

- **Source status:** Primary, final Code4rena report. The source is a public third-party audit, not a personal audit record.
- All root causes and reported impacts are summarized; original proof-of-concept code is not copied here.
- Each case contains a possible verification property. These are hypotheses for future formal checking, not independently executed tests.
- Selected findings concern Solidity contracts deployed on EVM-compatible chains. Where other chains appear in the original engagement, only the EVM-related case is included here.
