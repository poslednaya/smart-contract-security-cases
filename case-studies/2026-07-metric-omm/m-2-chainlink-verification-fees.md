# M-2 - Chainlink Data Streams fees are not paid during verification

**Severity:** Medium (final Sherlock report)  
**Contract:** `ChainlinkOracle.sol`  
**Category:** External integration, payment semantics, oracle liveness  
**Original report:** [Metric Sherlock final PDF, pp. 12-16](https://github.com/Metricxyz/Known_issues/blob/main/sherlock/2026.09.15%20-%20Final%20-%20Metric%20Public%20Bug%20Bounty%20Audit%20Contest%20Report%201789468517.pdf)  
**Original finding referenced in report:** https://github.com/sherlock-audit/2026-07-metric-judging/issues/141

## Root cause

The verification function calls `VerifierProxy.verify()` with a hardcoded zero native-token fee and passes an encoded `feeToken` address as metadata, but it does not implement a corresponding ERC-20 fee approval/payment path.

As a result, the contract is unable to pay a **nonzero native or token verification fee** in the paid Chainlink Data Streams configuration examined in the report. Valid report signatures alone do not make the update succeed.

## Conditions

- A real verifier bills a nonzero fee in native currency or an ERC-20 fee token.
- The pool depends on the Chainlink-backed feed.
- The previously stored report is approaching the configured staleness limit.

## Failure path

1. A pusher submits a valid signed report via `updateReport()` or `updateReports()`.
2. `ChainlinkOracle` invokes the verifier with no native fee and no ERC-20 approval/payment arrangement.
3. The verifier reverts on fee collection.
4. The oracle does not reach `_store()`, so the stored price is not refreshed.
5. Once the old report is stale, dependent price providers fail closed and affected pool swaps stop.

This is a **liveness / denial-of-service** issue in the intended fee-bearing deployment, not a demonstrated direct fund theft.

## Evidence in the original report

The supplied Foundry PoC uses a billing-aware **mock verifier** and tests both native-fee and ERC-20-fee cases. It shows that the implementation cannot pay either fee under the test assumptions. It does not claim a production incident.

## Reported remediation

Quote and forward the correct native verifier fee or implement safe ERC-20 funding and allowance/payment logic for the correct spender; batch updates need the fee for each report. The report lists [a fix commit](https://github.com/Oracle-Based-Pool/smart-contracts-poc/commit/fb3e4e407bf0bf535d418c68a7480e965e5f5e8c).

## Candidate verification property (not yet tested)

Under a **specified external verifier billing model**, and assuming the oracle holds sufficient funds and correct authorization, submission of a valid report with an accepted fee denomination should successfully reach storage. Without an explicit model of verifier payment and revert behavior, this property cannot be meaningfully proved by analyzing `ChainlinkOracle` bytecode alone.

## Attribution

This is a summary of a third-party published finding. See the Sherlock report for the original researchers, full PoC, discussion, and remediation details.
