# GTE Spot CLOB and Router

**Original engagement:** [Code4rena final findings and analysis](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router)  
**Published:** Feb 2026  
**Platform / stack:** EVM / Solidity  
**Focus:** Spot DEX / Order Book  
**Total findings in report:** 3 High, 4 Medium  
**Selected studies here:** 3

## Selected findings

| Finding | Technical issue | Final severity |
| --- | --- | --- |
| H-01 | [Doubly linked order list updated only in memory](h-01-prev-order-link-not-persisted.md) | High |
| H-02 | [Partially filled maker orders can become nontradeable dust](h-02-dust-maker-order-blocks-book.md) | High |
| H-03 | [Order amendments bypass per-transaction operation limits](h-03-amendment-bypasses-order-limit.md) | High |

## Notes

- **Source status:** Primary, final Code4rena report. The source is a public third-party audit, not a personal audit record.
- All root causes and reported impacts are summarized; original proof-of-concept code is not copied here.
- Each case contains a possible verification property. These are hypotheses for future formal checking, not independently executed tests.
- Selected findings concern Solidity contracts deployed on EVM-compatible chains. Where other chains appear in the original engagement, only the EVM-related case is included here.
