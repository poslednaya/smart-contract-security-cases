# M-3 - Truncated synthetic cross-price misprices low-ratio pools

**Severity:** Medium (final Sherlock report)  
**Contract:** `AnchoredPriceProvider.sol`  
**Category:** Integer rounding, oracle integration, financial loss  
**Original report:** [Metric Sherlock final PDF, pp. 17-24](https://github.com/Metricxyz/Known_issues/blob/main/sherlock/2026.09.15%20-%20Final%20-%20Metric%20Public%20Bug%20Bounty%20Audit%20Contest%20Report%201789468517.pdf)  
**Original finding referenced in report:** https://github.com/sherlock-audit/2026-07-metric-judging/issues/200

## Root cause

The synthetic price provider computes a cross-price from two 8-decimal USD feeds and **floors the quotient too early**:

```solidity
mid = Math.mulDiv(mid, ORACLE_DECIMALS, mid2); // ORACLE_DECIMALS = 1e8
```

For a low-priced base token against an expensive quote token, the true cross-price can be only ~1.9667 units in the 8-decimal representation. Integer flooring yields `1`, approximately 49% below the true cross-price. The pool then constructs its bid/ask band and swap curve around this already incorrect midpoint. Later directional rounding cannot recover discarded precision.

## Conditions

- Synthetic price mode is enabled (`quoteFeedId != 0`).
- The cheap base token / expensive quote token price ratio falls within a low E8 integer window.
- Liquidity exists on the base-token side of the pool.
- Narrow configured spreads do not cover the large truncation error.
- The oracle prices are otherwise fresh and correct; oracle manipulation is not required.

## Exploit path

1. Honest oracle feeds provide two USD prices.
2. The provider truncates the synthetic cross-price.
3. The pool quotes the base token materially below its true value.
4. An arbitrageur buys base-side inventory through a swap.
5. The LP holds the underpaid quote asset and loses the difference.

## Impact shown by the original report

The report's Foundry PoC values the pool at approximately **$9,440 before** and **$4,830 after** a swap, with approximately **$4,609.75 of LP principal lost** (roughly 48% of that test pool's value). These are reported test results, not an independent reproduction.

**Note:** The discussion considers a higher severity, but the *final audit report records the finding as M-3 (Medium)*. This portfolio follows the final classification.

## Reported remediation

Keep more precision through cross-price calculation before band construction, or otherwise conservatively bound the rounding error. The Sherlock report lists a team fix in [Oracle-Based-Pool/smart-contracts-poc PR #15](https://github.com/Oracle-Based-Pool/smart-contracts-poc/pull/15).

## Candidate verification property (not yet tested)

For valid oracle prices, the executable bid/ask band should remain within the intended configured bounds around a sufficiently precise synthetic cross-price, **including quantization error**. This requires treating oracle price tuples as constrained inputs and proving sound lower/upper bounds rather than equating a floored integer with the exact economic price.

## Attribution

This is a summary of a third-party published finding. See the Sherlock report for the original researchers, full PoC, discussion, and remediation details.
