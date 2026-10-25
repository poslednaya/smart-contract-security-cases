# M-02: Cross-chain minimum amount ignores LayerZero dust truncation

**Project:** Brix Money  
**Platform / stack:** EVM / Solidity  
**Severity:** Medium (final Code4rena report)  
**Source:** [Brix Money - Code4rena final report](https://code4rena.com/reports/2025-11-brix-money) (finding `M-02`)  
**Scope:** wiTryVaultComposer / LayerZero OFTCore

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The unstake and fast redeem paths set minAmountLD equal to exact assets while OFTCore._removeDust truncates the amount to shared token precision.

## Impact reported by Code4rena

Operations revert with SlippageExceeded whenever the amount contains nonzero conversion dust.

## Suggested mitigation / review direction

Use dust-adjusted output for the minimum or explicitly validate and report unsupported amounts.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

For any admissible asset quantity, the minimum bridge output must not exceed the value remaining after the protocol's documented decimal truncation.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2025-11-brix-money](https://code4rena.com/reports/2025-11-brix-money). Locate section **M-02** in that report.
