# H-02: Liquidation reentrancy turns phantom shares into real shares

**Project:** Panoptic: Next Core  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Panoptic: Next Core - Code4rena final report](https://code4rena.com/reports/2025-12-panoptic-next-core) (finding `H-02`)  
**Scope:** PanopticPool._liquidate / CollateralTracker.settleLiquidation

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

During liquidation, phantom share delegations for two collateral trackers are revoked sequentially. An external ETH refund occurs while phantom shares remain available in the other tracker, and the revoke logic can compensate missing phantom shares with real internal supply.

## Impact reported by Code4rena

Reentrant liquidator can convert synthetic voting/solvency shares into redeemable shares and drain collateral tracker assets.

## Suggested mitigation / review direction

Apply a shared reentrancy lock and complete all phantom-share revocations before external callbacks; avoid compensating transferred phantom balances.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

During liquidation, no externally callable interleaving may convert phantom shares into redeemable supply; phantom share creation and revocation must be atomic across both trackers.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-12-panoptic-next-core](https://code4rena.com/reports/2025-12-panoptic-next-core). Locate section **H-02** in that report.
