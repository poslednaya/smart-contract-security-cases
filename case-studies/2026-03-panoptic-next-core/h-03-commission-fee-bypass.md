# H-03: Commission fee is bypassed in option burn settlement

**Project:** Panoptic: Next Core  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Panoptic: Next Core - Code4rena final report](https://code4rena.com/reports/2025-12-panoptic-next-core) (finding `H-03`)  
**Scope:** CollateralTracker.settleBurn / PanopticPool

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

CollateralTracker.settleBurn computes commission from the minimum of premium and notional fees; the report shows transaction paths where this computation permits a commission below the intended charge.

## Impact reported by Code4rena

The protocol under-collects commission in affected exercise or settlement flows.

## Suggested mitigation / review direction

Make commission assessment independent of bypassable intermediate representations and test all burn call paths.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

Every option burn with an applicable configured commission must accrue at least the correct fee for the realized notional/premium under policy.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-12-panoptic-next-core](https://code4rena.com/reports/2025-12-panoptic-next-core). Locate section **H-03** in that report.
