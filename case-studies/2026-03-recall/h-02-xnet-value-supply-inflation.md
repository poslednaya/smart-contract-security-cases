# H-02: Value-bearing Xnet calls inflate child-subnet circulating supply

**Project:** Recall  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Recall - Code4rena final report](https://code4rena.com/reports/2025-02-recall) (finding `H-02`)  
**Scope:** CheckpointingFacet / cross-network message handling

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The IPC accounting path for Xnet messages carrying nonzero value mishandles circulation updates between subnets, so reported child supply can increase beyond economically backed transfers.

## Impact reported by Code4rena

Cross-subnet issuance/accounting can diverge from collateralization and supply invariants.

## Suggested mitigation / review direction

Align circulating-supply deltas with actual escrow, mint, burn, and acknowledgement events.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

A cross-network value message must conserve net bridged value across all supply and escrow ledgers, including completion and failure outcomes.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-02-recall](https://code4rena.com/reports/2025-02-recall). Locate section **H-02** in that report.
