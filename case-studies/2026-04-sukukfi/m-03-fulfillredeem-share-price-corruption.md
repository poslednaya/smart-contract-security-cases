# M-03: fulfillRedeem can distort share price and permit over-redemption

**Project:** SukukFi  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [SukukFi - Code4rena final report](https://code4rena.com/reports/2025-11-sukukfi) (finding `M-03`)  
**Scope:** ERC7575VaultUpgradeable.fulfillRedeem

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The report identifies inconsistent share/asset accounting during fulfilment of asynchronous redemption claims, affecting the circulating supply and reserved asset calculations used for price per share.

## Impact reported by Code4rena

Subsequent redemption paths can over-allocate assets to claimants at the expense of remaining depositors.

## Suggested mitigation / review direction

Reconcile the share burning and asset reserving transitions atomically and test accounting conservation across pending-to-claimable states.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

Pending and claimable redemptions must be counted exactly once in both supply and asset accounting; fulfill should preserve the appropriate PPS invariant.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-11-sukukfi](https://code4rena.com/reports/2025-11-sukukfi). Locate section **M-03** in that report.
