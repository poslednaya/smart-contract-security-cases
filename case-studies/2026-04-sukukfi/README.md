# SukukFi

**Original engagement:** [Code4rena final findings and analysis](https://code4rena.com/reports/2025-11-sukukfi)  
**Published:** Apr 2026  
**Platform / stack:** EVM / Solidity  
**Focus:** Async Vault / ERC-7575  
**Total findings in report:** 1 High, 3 Medium  
**Selected studies here:** 3

## Selected findings

| Finding | Technical issue | Final severity |
| --- | --- | --- |
| H-01 | [Third party can withdraw another holder’s approved shares](h-01-vault-withdrawal-authorization.md) | High |
| M-02 | [Locked-in redemption prices become stale liabilities](m-02-stale-redemption-liability.md) | Medium |
| M-03 | [fulfillRedeem can distort share price and permit over-redemption](m-03-fulfillredeem-share-price-corruption.md) | Medium |

## Notes

- **Source status:** Primary, final Code4rena report. The source is a public third-party audit, not a personal audit record.
- All root causes and reported impacts are summarized; original proof-of-concept code is not copied here.
- Each case contains a possible verification property. These are hypotheses for future formal checking, not independently executed tests.
- Selected findings concern Solidity contracts deployed on EVM-compatible chains. Where other chains appear in the original engagement, only the EVM-related case is included here.
