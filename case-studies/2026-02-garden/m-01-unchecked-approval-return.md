# M-01: Unchecked ERC20 approval failure can strand HTLC deposits

**Project:** Garden  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [Garden - Code4rena final report](https://code4rena.com/reports/2025-11-garden) (finding `M-01`)  
**Scope:** swap/UDA.sol initialize

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

UniqueDepositAddress.initialize ignores a false return from token.approve. The contract proceeds to initiate the HTLC despite the absent allowance and marks the address initialized.

## Impact reported by Code4rena

With tokens that signal approval failure by returning false, transfer setup fails and deposited funds may remain permanently locked.

## Suggested mitigation / review direction

Use checked ERC20 approval calls and only finalize initialization after token transfer conditions are met.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

A successful initialization implying an HTLC deposit must ensure the token allowance/transfer precondition actually succeeded.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-11-garden](https://code4rena.com/reports/2025-11-garden). Locate section **M-01** in that report.
