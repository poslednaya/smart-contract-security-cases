# M-8 - Low-precision stop-loss metric fails to stop a large drawdown

**Severity:** Medium (final Sherlock report)  
**Contract:** `OracleValueStopLossExtension.sol`  
**Category:** Fixed-point precision, protective invariant  
**Original report:** [Metric Sherlock final PDF, pp. 59-66](https://github.com/Metricxyz/Known_issues/blob/main/sherlock/2026.09.15%20-%20Final%20-%20Metric%20Public%20Bug%20Bounty%20Audit%20Contest%20Report%201789468517.pdf)  
**Original finding referenced in report:** https://github.com/sherlock-audit/2026-07-metric-judging/issues/3048

## Root cause

`_metrics()` calculates token-denominated values per share using the fixed `METRIC_SCALE = 1e6` and integer division. For expensive numeraire assets such as WBTC, a meaningful change in economic value may disappear in the integer-valued metric. `_applyWatermark()` also floors the threshold and uses a strict comparison.

The report's example gives a high-watermark metric of `8` and a live metric of `7`. A 5% stop-loss threshold is also floored to `7`, so `7 < 7` is false and the protective check does not trigger.

## Conditions

- An LP uses the stop-loss extension in a USDC/WBTC pool.
- The stop-loss threshold is configured at 5%.
- Oracle repricing and pool state yield a true protected-leg drawdown greater than 10%, even though the scaled metric changes by only one integer unit.

## Failure path

1. Liquidity is deposited and a high-watermark is stored.
2. WBTC is honestly repriced from $100,000 to $125,000 in the example.
3. A swap begins the loss-making protected leg.
4. The precise loss exceeds the configured 5% drawdown threshold.
5. Integer rounding makes the measured metric equal the floored stop-loss threshold.
6. The extension accepts the swap instead of stopping it.

## Impact shown by the original report

The report demonstrates a **10.025%** drawdown on the relevant protected-leg metric, bypassing a configured **5%** stop-loss. In the subsequent PoC cycle the LP loses about **$567.63**, or **0.025235% of principal**. Note that these percentages measure *different quantities*: protected-leg drawdown versus total LP principal loss.

## Reported remediation

Retain sufficient precision in per-share metrics and compare the current value to the watermark using a cross-multiplication formulation that cannot hide the configured threshold through flooring. The report links to [Metric-OMM/metric-periphery PR #49](https://github.com/Metric-OMM/metric-periphery/pull/49).

## Candidate verification property (not yet tested)

Whenever the protected economic value drops below the configured threshold relative to a positive high watermark, an otherwise executable protected swap must revert or invoke the specified stop-loss action. The proof needs a carefully defined full-precision valuation and should examine all reachable input scales and rounding boundaries.

## Attribution

This is a summary of a third-party published finding. See the Sherlock report for the original researchers, full PoC, discussion, and remediation details.
