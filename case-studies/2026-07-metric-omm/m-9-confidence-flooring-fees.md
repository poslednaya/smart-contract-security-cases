# M-9 - Early E8 rounding erases part of the configured swap fee

**Severity:** Medium (final Sherlock report)  
**Contract:** `AnchoredPriceProvider.sol`  
**Category:** Oracle confidence handling, rounding, fee accounting  
**Original report:** [Metric Sherlock final PDF, pp. 67-73](https://github.com/Metricxyz/Known_issues/blob/main/sherlock/2026.09.15%20-%20Final%20-%20Metric%20Public%20Bug%20Bounty%20Audit%20Contest%20Report%201789468517.pdf)  
**Original finding referenced in report:** https://github.com/sherlock-audit/2026-07-metric-judging/issues/3894

## Root cause

`_shapedQuote()` computes a confidence-derived delta in the coarse E8 price representation and floors it **before** converting the quote to the higher-precision Q64.64 domain. With a low-priced asset, the confidence delta can be fractional in E8 units and become zero.

In the reported example:

```text
E8 midpoint       = 299
oracle spread      = 21 bps
confidence delta   = 0.6279 E8 units
stored E8 delta    = 0
```

The premature rounding removes the confidence-based widening of the executable bid/ask band. The fallback minimum band is insufficient to recover the missing configured fee contribution.

## Conditions

- A mutable `AnchoredPriceProvider` uses a low-E8-priced asset.
- A nonzero confidence parameter is configured together with margin step settings for which confidence widening should exceed the mandatory anchored clamp.
- Fresh and otherwise correct oracle values produce a fractional confidence delta in E8 units.

## Failure path

1. The oracle reports a correct low-price midpoint and uncertainty spread.
2. The confidence contribution is calculated, then rounded down to zero.
3. The returned executable bid is too high and the ask too low relative to the higher-precision intended band.
4. Swaps use an understated base fee and distribute less fee revenue to LPs / configured recipients.

## Impact shown by the original report

The source PoC compares **21.523162 bps charged** with **31.048134 bps** from the precision-preserving calculation, implying **30.678% of the expected base-fee yield omitted** for the demonstrated configuration. This is not a claim about 30.678% of total pool revenue across all configurations.

## Reported remediation

Carry the confidence numerator through Q64.64 bid/ask conversion and round only at the final bound (bid down, ask up). The report links to [this fix commit](https://github.com/Oracle-Based-Pool/smart-contracts-poc/commit/e55b4666ca57a51476e1550661c2ae8957ae3e40).

## Candidate verification property (not yet tested)

For all valid feed states and accepted provider configurations, the low-precision executable bid should be no higher and the ask no lower than conservative price bounds obtained with full intermediate precision and documented fee settings. Check near-zero and sub-unit confidence contributions in particular.

## Attribution

This is a summary of a third-party published finding. See the Sherlock report for the original researchers, full PoC, discussion, and remediation details.
