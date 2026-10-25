# H-03: Incorrect hash prevents cross-chain receipt execution

**Project:** Recall  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Recall - Code4rena final report](https://code4rena.com/reports/2025-02-recall) (finding `H-03`)  
**Scope:** IpcContract.sol

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

IpcContract.sol relies on an inconsistent or wrong hash to correlate a cross-chain message with its receipt during processing.

## Impact reported by Code4rena

Receipt execution can fail and leave funds locked or permanently inaccessible.

## Suggested mitigation / review direction

Canonicalize hash construction and test round-trip message/receipt identity across send and receive.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

Any emitted outbound message ID must equal the ID used for its corresponding verified inbound receipt under identical message data.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-02-recall](https://code4rena.com/reports/2025-02-recall). Locate section **H-03** in that report.
