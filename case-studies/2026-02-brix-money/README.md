# Brix Money

**Original engagement:** [Code4rena final findings and analysis](https://code4rena.com/reports/2025-11-brix-money)  
**Published:** Feb 2026  
**Platform / stack:** EVM / Solidity  
**Focus:** Cross-chain Staking / Vault  
**Total findings in report:** 0 High, 3 Medium  
**Selected studies here:** 3

## Selected findings

| Finding | Technical issue | Final severity |
| --- | --- | --- |
| M-01 | [Composer path bypasses restricted-staker policy](m-01-cross-chain-restriction-bypass.md) | Medium |
| M-02 | [Cross-chain minimum amount ignores LayerZero dust truncation](m-02-layerzero-dust-minamount-revert.md) | Medium |
| M-03 | [Cross-chain unstaking assumes sender and recipient addresses match](m-03-cross-chain-address-symmetry.md) | Medium |

## Notes

- **Source status:** Primary, final Code4rena report. The source is a public third-party audit, not a personal audit record.
- All root causes and reported impacts are summarized; original proof-of-concept code is not copied here.
- Each case contains a possible verification property. These are hypotheses for future formal checking, not independently executed tests.
- Selected findings concern Solidity contracts deployed on EVM-compatible chains. Where other chains appear in the original engagement, only the EVM-related case is included here.
