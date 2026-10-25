# M-02: Locked-in redemption prices become stale liabilities

**Project:** SukukFi  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [SukukFi - Code4rena final report](https://code4rena.com/reports/2025-11-sukukfi) (finding `M-02`)  
**Scope:** ERC7575VaultUpgradeable.fulfillRedeem

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

fulfillRedeem locks assets owed at the then-current price per share, but the user need not claim immediately; later asset losses do not automatically reprice the reserved claim.

## Impact reported by Code4rena

Remaining shareholders can disproportionately absorb subsequent asset losses and redemption obligations may outgrow available assets.

## Suggested mitigation / review direction

Specify and enforce how async claims absorb portfolio changes; reconcile all outstanding claim liabilities with realizable assets.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

After any valuation change, total fulfilled and outstanding redemption liabilities must remain backed without misallocating unrealized gains or losses to other holders.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-11-sukukfi](https://code4rena.com/reports/2025-11-sukukfi). Locate section **M-02** in that report.
