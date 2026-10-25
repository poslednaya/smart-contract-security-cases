# H-02: Partially filled maker orders can become nontradeable dust

**Project:** GTE Spot CLOB and Router  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [GTE Spot CLOB and Router - Code4rena final report](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router) (finding `H-02`)  
**Scope:** CLOB.sol partial matching

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

A maker order can be partially filled below the minimum amount without removal; subsequent matching rounds quote consideration to zero and triggers ZeroCostTrade.

## Impact reported by Code4rena

Residual dust orders block otherwise valid incoming orders and degrade order-book availability.

## Suggested mitigation / review direction

Prune dust orders on partial fills or safely skip them during matching.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

After each match, all surviving orders must be eligible for nonzero-value execution or must be removed / explicitly skipped.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-07-gte-spot-clob-and-router](https://code4rena.com/reports/2025-07-gte-spot-clob-and-router). Locate section **H-02** in that report.
