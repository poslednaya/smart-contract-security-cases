# H-01: BuilderWallet can be re-initialized and seized

**Project:** Panoptic: Next Core  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Panoptic: Next Core - Code4rena final report](https://code4rena.com/reports/2025-12-panoptic-next-core) (finding `H-01`)  
**Scope:** BuilderWallet.init

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

BuilderWallet.init is insufficiently protected against calls after deployment, allowing an attacker to replace the wallet administrator.

## Impact reported by Code4rena

An attacker can take control and sweep accumulated builder-wallet ERC20 fees.

## Suggested mitigation / review direction

Enforce one-time initialization and bind the authorized initializer to deployment or factory control.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

For any successfully initialized wallet, all later calls to init must fail or leave owner/admin unchanged.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-12-panoptic-next-core](https://code4rena.com/reports/2025-12-panoptic-next-core). Locate section **H-01** in that report.
