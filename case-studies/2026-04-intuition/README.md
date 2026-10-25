# Intuition

**Original engagement:** [Code4rena final findings and analysis](https://code4rena.com/reports/2026-03-intuition)  
**Published:** Apr 2026  
**Platform / stack:** EVM / Solidity  
**Focus:** Account Abstraction / Emissions  
**Total findings in report:** 0 High, 2 Medium  
**Selected studies here:** 2

## Selected findings

| Finding | Technical issue | Final severity |
| --- | --- | --- |
| M-01 | [Validity window omitted from signed user-operation digest](m-01-unsigned-signature-validity-window.md) | Medium |
| M-02 | [New-epoch checkpoint is counted in previous-epoch rewards](m-02-inclusive-epoch-snapshot.md) | Medium |

## Notes

- **Source status:** Primary, final Code4rena report. The source is a public third-party audit, not a personal audit record.
- All root causes and reported impacts are summarized; original proof-of-concept code is not copied here.
- Each case contains a possible verification property. These are hypotheses for future formal checking, not independently executed tests.
- Selected findings concern Solidity contracts deployed on EVM-compatible chains. Where other chains appear in the original engagement, only the EVM-related case is included here.
