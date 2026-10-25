# M-01: Validity window omitted from signed user-operation digest

**Project:** Intuition  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [Intuition - Code4rena final report](https://code4rena.com/reports/2026-03-intuition) (finding `M-01`)  
**Scope:** AtomWallet._validateSignature

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

AtomWallet extracts validAfter/validUntil from the signature suffix but verifies the ECDSA signature over userOpHash without binding these metadata fields. A relayer can change the timestamps without invalidating the signature.

## Impact reported by Code4rena

Signed operations can be presented beyond the validity limits intended by the account owner.

## Suggested mitigation / review direction

Bind validity fields to the signed hash and reject modified suffixes.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

Altering any signed operation policy field, including its validity window, must invalidate signature verification.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2026-03-intuition](https://code4rena.com/reports/2026-03-intuition). Locate section **M-01** in that report.
