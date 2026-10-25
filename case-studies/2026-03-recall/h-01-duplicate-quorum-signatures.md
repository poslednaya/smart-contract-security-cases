# H-01: Duplicate validator signatures count repeatedly toward quorum

**Project:** Recall  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Recall - Code4rena final report](https://code4rena.com/reports/2025-02-recall) (finding `H-01`)  
**Scope:** SubnetActorCheckpointingFacet.submitCheckpoint

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

submitCheckpoint passes arrays of signatories to weighted signature validation without enforcing address uniqueness, so the same validator signature and weight can be counted repeatedly.

## Impact reported by Code4rena

A malicious minority validator may satisfy quorum and submit an unauthorized checkpoint.

## Suggested mitigation / review direction

Reject duplicate signatory identities before weight accumulation.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

The cumulative quorum weight must be computed from distinct authorized validators, each contributing at most once.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-02-recall](https://code4rena.com/reports/2025-02-recall). Locate section **H-01** in that report.
