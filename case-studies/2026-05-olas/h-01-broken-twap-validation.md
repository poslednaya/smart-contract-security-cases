# H-01: Broken TWAP validation defeats price-deviation protection

**Project:** Olas  
**Platform / stack:** EVM / Solidity  
**Severity:** High (final Code4rena report)  
**Source:** [Olas - Code4rena final report](https://code4rena.com/reports/2026-01-olas) (finding `H-01`)  
**Scope:** Protocol-owned liquidity / TWAP checks

> **Provenance:** This is an independently written study of a **third-party published finding**, not my own audit submission. The PoC and reported impact have not been independently reproduced for this collection.

## Root cause

The report identifies faulty validation of the reference TWAP against manipulable spot quotes in the protocol-owned liquidity flow. This permits price-sensitive operations to rely on an insufficiently protected market price.

## Impact reported by Code4rena

An attacker can exploit manipulated spot conditions while intended TWAP and slippage protections fail to reject the action.

## Suggested mitigation / review direction

Restore independent TWAP computation and enforce the deviation/slippage checks on the actual execution price.

This is a concise mitigation direction based on the published finding; consult the source for the team's actual patch and adjudication.

## Candidate verification property (not yet tested)

A price-sensitive action must reject spot prices outside the configured deviation from an independently sourced and correctly computed TWAP.

This is a proposed check for a future test or prover specification, **not** evidence that `pevm` has detected or verified the vulnerability. The proposed property still requires a correct EVM-level specification and has not been proven.

## Attribution

Original finding, detailed reasoning, proof of concept and any listed submitters or sponsors: [https://code4rena.com/reports/2026-01-olas](https://code4rena.com/reports/2026-01-olas). Locate section **H-01** in that report.
