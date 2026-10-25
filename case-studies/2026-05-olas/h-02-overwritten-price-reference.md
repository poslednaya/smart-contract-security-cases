# H-02: Overwritten reference makes price deviation check ineffective

**Project:** Olas  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Olas - Code4rena final report](https://code4rena.com/reports/2026-01-olas) (finding `H-02`)  
**Scope:** checkPoolAndGetCenterPrice

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

In checkPoolAndGetCenterPrice(), a value intended to preserve an independently measured center price is overwritten, making the subsequent deviation comparison ineffective.

## Impact reported by Code4rena

V3 protocol-owned liquidity operations can proceed without the intended deviation defense.

## Suggested mitigation / review direction

Keep a distinct immutable local reference for the independent price and test meaningful deviations.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

The reference price used in deviation validation must be independent of the candidate price and must not be overwritten along the check path.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2026-01-olas](https://code4rena.com/reports/2026-01-olas). Locate section **H-02** in that report.
