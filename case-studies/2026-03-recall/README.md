# Recall

**Original engagement:** [Code4rena final findings and analysis](https://code4rena.com/reports/2025-02-recall)  
**Published:** Mar 2026  
**Platform / stack:** EVM / Solidity  
**Focus:** Cross-chain / IPC  
**Total findings in report:** See report for all findings  
**Selected studies here:** 3

## Selected findings

| Finding | Technical issue | Final severity |
| --- | --- | --- |
| H-01 | [Duplicate validator signatures count repeatedly toward quorum](h-01-duplicate-quorum-signatures.md) | High |
| H-02 | [Value-bearing Xnet calls inflate child-subnet circulating supply](h-02-xnet-value-supply-inflation.md) | High |
| H-03 | [Incorrect hash prevents cross-chain receipt execution](h-03-incorrect-cross-chain-message-hash.md) | High |

## Notes

- **Source status:** Primary, final Code4rena report. The source is a public third-party audit, not a personal audit record.
- All root causes and reported impacts are summarized; original proof-of-concept code is not copied here.
- Each case contains a possible verification property. These are hypotheses for future formal checking, not independently executed tests.
- Selected findings concern Solidity contracts deployed on EVM-compatible chains. Where other chains appear in the original engagement, only the EVM-related case is included here.
