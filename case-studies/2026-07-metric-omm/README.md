# Metric OMM - Sherlock Public Bug Bounty Audit Contest

- **Audit period:** July 6-27, 2026
- **Report publication:** September 15, 2026
- **Category:** Oracle-based DEX / AMM
- **Environment:** EVM smart contracts
- **Final report totals:** 0 High, 9 Medium
- **Selected here:** 5 Medium case studies
- **Status of this write-up:** Report-based research notes; the original PoCs have **not** been rerun independently.

**Sources:** [Sherlock contest](https://audits.sherlock.xyz/contests/1279) | [Official public audit report (PDF)](https://github.com/Metricxyz/Known_issues/blob/main/sherlock/2026.09.15%20-%20Final%20-%20Metric%20Public%20Bug%20Bounty%20Audit%20Contest%20Report%201789468517.pdf) | [Metric's audit repository](https://github.com/Metricxyz/Known_issues)

## Selected case studies

| ID | Vulnerability | Root-cause category | Impact reported in PoC | Case study |
| --- | --- | --- | --- | --- |
| M-3 | Truncated synthetic cross price | Integer arithmetic / oracle pricing | ~$4,609.75 LP loss | [Read](m-3-synthetic-cross-price.md) |
| M-5 | Zero-output exact-input swaps move the cursor | State inconsistency / swap math | ~$33.08 LP loss | [Read](m-5-zero-output-cursor-drift.md) |
| M-8 | Stop-loss fails to recognize a >10% drawdown | Precision loss / safety check | ~$567.63 LP loss | [Read](m-8-stop-loss-precision.md) |
| M-9 | Confidence delta rounded away | Fee accounting / fixed-point math | ~30.68% of expected base-fee yield omitted | [Read](m-9-confidence-flooring-fees.md) |
| M-2 | Chainlink Data Streams verification fee unpaid | Oracle integration / liveness | Feed update reverts; dependent swaps can stall | [Read](m-2-chainlink-verification-fees.md) |

## Why these five?

They demonstrate distinct failure modes: incorrect oracle-derived prices, state changes with zero token transfers, a bypassed financial protection invariant, fee under-collection, and dependence on external verifier billing semantics.

## Attribution and scope

This is **not** a claim of participation in the Metric contest, discovery of these vulnerabilities, or independent exploit reproduction. Each finding is credited to the original Sherlock report and its listed researchers. The numbers below are *reported PoC results*, not new test results.

The final report labels all five selected issues **Medium**, including M-3, whose discussion considers stronger severity. Remediation references below document what the report says was fixed; they do not constitute an independent review of the patch.

## Formal verification angle

Every case includes a **candidate verification property** suitable for further investigation. A useful proof would have to specify the actual EVM implementation, inputs, state invariants, external-call behavior, and the exact relationship between model abstractions and executable bytecode. These properties are hypotheses and **have not been proved with `pevm`**.

## Source

Sherlock, *Security Review for Metric: Public Bug Bounty Audit Contest* (audit July 6-27, 2026), [PDF](https://github.com/Metricxyz/Known_issues/blob/main/sherlock/2026.09.15%20-%20Final%20-%20Metric%20Public%20Bug%20Bounty%20Audit%20Contest%20Report%201789468517.pdf). See the PDF page ranges within individual cases.
