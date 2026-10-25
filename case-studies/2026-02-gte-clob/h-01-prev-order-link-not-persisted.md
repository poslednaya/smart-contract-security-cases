# H-01: Doubly linked order list updated only in memory

**Project:** GTE Spot CLOB and Router  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [GTE Spot CLOB and Router - Code4rena final report](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router) (finding `H-01`)  
**Scope:** Book.sol _updateLimitPostOrder

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

When adding a new order, _updateLimitPostOrder sets order.prevOrderId in a memory struct, without persisting the modified field to self.orders storage.

## Impact reported by Code4rena

Removing orders corrupts head/tail links and can prevent further order posting or cancellation.

## Suggested mitigation / review direction

Persist predecessor fields to the stored order, not only a memory copy.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

For any nonempty price-level order list, adjacent stored orders must have mutually consistent next/prev links after insertion, removal, and matching.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-07-gte-spot-clob-and-router](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router). Locate section **H-01** in that report.
