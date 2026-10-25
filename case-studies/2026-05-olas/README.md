# Olas

**Original engagement:** [Code4rena final findings and analysis](https://code4rena.com/reports/2026-01-olas)  
**Published:** May 2026  
**Platform / stack:** EVM / Solidity  
**Focus:** Oracle / Protocol-owned Liquidity  
**Total findings in report:** 11 High, 12 Medium  
**Selected studies here:** 3

## Selected findings

| Finding | Technical issue | Final severity |
| --- | --- | --- |
| H-01 | [Broken TWAP validation defeats price-deviation protection](h-01-broken-twap-validation.md) | High |
| H-02 | [Overwritten reference makes price deviation check ineffective](h-02-overwritten-price-reference.md) | High |
| H-03 | [Balancer oracle prices assets using steerable vault balances](h-03-balancer-oracle-manipulable-balances.md) | High |

## Notes

- **Source status:** Primary, final Code4rena report. The source is a public third-party audit, not a personal audit record.
- All root causes and reported impacts are summarized; original proof-of-concept code is not copied here.
- Each case contains a possible verification property. These are hypotheses for future formal checking, not independently executed tests.
- Selected findings concern Solidity contracts deployed on EVM-compatible chains. Where other chains appear in the original engagement, only the EVM-related case is included here.
