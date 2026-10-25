# M-03: Cross-chain unstaking assumes sender and recipient addresses match

**Project:** Brix Money  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [Brix Money - Code4rena final report](https://code4rena.com/reports/2025-11-brix-money) (finding `M-03`)  
**Scope:** Cross-chain unstaking

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The cross-chain unstaking flow enforces address symmetry that cannot be guaranteed for multisig wallets and account-abstraction users deployed at differing chain addresses.

## Impact reported by Code4rena

Legitimate AA and multisig users may be unable to execute unstaking even when they own valid claims.

## Suggested mitigation / review direction

Separate permission checks from address-equality requirements; support explicit recipient authorizations.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

Cross-chain withdrawals should be authorized by a verifiable sender-to-beneficiary relation, not by assumed address equality across domains.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-11-brix-money](https://code4rena.com/reports/2025-11-brix-money). Locate section **M-03** in that report.
