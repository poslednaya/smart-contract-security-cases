# Centrifuge Protocol V3.1

- **Engagement:** [Sherlock contest #1028](https://audits.sherlock.xyz/contests/1028)
- **Date:** Oct-Nov 2025
- **Category:** RWA / Cross-chain
- **Source status:** Official report location confirmed; selected mechanisms corroborated via secondary disclosures
- **Official report:** [Open report](https://github.com/centrifuge/protocol/blob/main/docs/audits/2025-12-Sherlock-Blackthorn.pdf)

## Selected case studies

| ID | Technical issue | Severity |
| --- | --- | --- |
| H-1 (secondary) | [Mutable request manager may redirect pending deposits across pools](request-manager-escrow-mismatch.md) | High (secondary source) |
| M (secondary) | [ETH attached to a batched bridge call becomes stranded](batched-bridge-ether-stranding.md) | Medium (secondary source) |
| M (secondary) | [Unbounded cross-chain batch message count can trigger DoS](unbounded-gateway-batch.md) | Medium (secondary source) |

## Scope and attribution

These are annotated studies of published findings by other researchers, not personal audit credits. Severity is transcribed from the primary report when available; otherwise it is labelled as secondary. The verification angles are proposed proof obligations, not assertions that `pevm` found or proved the cases.
