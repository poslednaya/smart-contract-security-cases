# M-02: New-epoch checkpoint is counted in previous-epoch rewards

**Project:** Intuition  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [Intuition - Code4rena final report](https://code4rena.com/reports/2026-03-intuition) (finding `M-02`)  
**Scope:** CoreEmissionsController / TrustBonding / VotingEscrow

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The snapshot timestamp epochTimestampEnd(N) coincides with the start of epoch N+1, while VotingEscrow historical lookup includes checkpoints at ts <= boundary.

## Impact reported by Code4rena

A user creating or extending a lock at the start of the next epoch can obtain a share of the previous epoch's rewards despite not being bonded then.

## Suggested mitigation / review direction

Define exclusive snapshot boundaries or query an in-epoch cutoff consistently throughout emissions accounting.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

Rewards for epoch N must be computed from stake effective strictly before epoch N+1 begins.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2026-03-intuition](https://code4rena.com/reports/2026-03-intuition). Locate section **M-02** in that report.
