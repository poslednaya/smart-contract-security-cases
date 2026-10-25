# H-03: Order amendments bypass per-transaction operation limits

**Project:** GTE Spot CLOB and Router  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [GTE Spot CLOB and Router - Code4rena final report](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router) (finding `H-03`)  
**Scope:** Order amendments / maxLimitsPerTx

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The amendment pathway can be invoked repeatedly without consistently charging against maxLimitsPerTx constraints designed to bound order-book operations.

## Impact reported by Code4rena

An attacker can force excessive work in one call or sequence and deny service to matching operations.

## Suggested mitigation / review direction

Charge amendments to the shared operation budget and enforce bounds before each mutation.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

All order operations, including create, cancel, and amend, must account for resource limits under a consistent transaction budget.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-07-gte-spot-clob-and-router](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router). Locate section **H-03** in that report.
