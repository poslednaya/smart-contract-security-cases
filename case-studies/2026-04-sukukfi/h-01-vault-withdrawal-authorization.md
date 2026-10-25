# H-01: Third party can withdraw another holder’s approved shares

**Project:** SukukFi  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [SukukFi - Code4rena final report](https://code4rena.com/reports/2025-11-sukukfi) (finding `H-01`)  
**Scope:** WERC7575Vault._withdraw / share allowance

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

WERC7575Vault.withdraw/redeem invokes a share-token permission check on the vault allowance but does not authorize msg.sender relative to owner. When owner authorized the vault, an arbitrary caller can direct the assets to a chosen receiver.

## Impact reported by Code4rena

Unauthorized withdrawal or redemption of a user's shares and theft of underlying assets.

## Suggested mitigation / review direction

Require msg.sender == owner or implement correct owner-to-caller allowance handling.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

If caller is not owner, redemption must require and consume an authorization from owner to that caller, not merely to the vault.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-11-sukukfi](https://code4rena.com/reports/2025-11-sukukfi). Locate section **H-01** in that report.
