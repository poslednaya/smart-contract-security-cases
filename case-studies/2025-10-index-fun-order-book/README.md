# Index Fun Order Book

- **Engagement:** [Sherlock contest #1197](https://audits.sherlock.xyz/contests/1197)
- **Date:** Oct 2025
- **Category:** Order Book / Prediction Markets
- **Source status:** Secondary disclosures; primary PDF not located

## Selected case studies

| ID | Technical issue | Severity |
| --- | --- | --- |
| H-1 | [Seller is charged the buyer's trade fee](seller-pays-buyer-fee.md) | High |
| M (source) | [No emergency invalidation path for unresolved markets](missing-market-invalidation.md) | Medium (secondary source) |
| M (source) | [Emergency resolution targets the live epoch instead of the intended epoch](wrong-epoch-emergency-resolution.md) | Medium (secondary source) |

## Scope and attribution

These are annotated studies of published findings by other researchers, not personal audit credits. Severity is transcribed from the primary report when available; otherwise it is labelled as secondary. The verification angles are proposed proof obligations, not assertions that `pevm` found or proved the cases.
