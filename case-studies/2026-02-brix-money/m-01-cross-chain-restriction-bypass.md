# M-01: Composer path bypasses restricted-staker policy

**Project:** Brix Money  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [Brix Money - Code4rena final report](https://code4rena.com/reports/2025-11-brix-money) (finding `M-01`)  
**Scope:** wiTryVaultComposer / StakediTryCrosschain

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The cross-chain LayerZero composer deposits under its own caller identity while the protocol does not propagate the original beneficiary's staking restrictions through the compose path.

## Impact reported by Code4rena

A restricted user can receive cross-chain staking exposure that direct staking would have blocked.

## Suggested mitigation / review direction

Apply policy checks to originating user identity in all composition and deposit routes.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

For every deposit route, including asynchronous cross-chain messages, role restrictions must apply to the economic beneficiary and original depositor.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-11-brix-money](https://code4rena.com/reports/2025-11-brix-money). Locate section **M-01** in that report.
