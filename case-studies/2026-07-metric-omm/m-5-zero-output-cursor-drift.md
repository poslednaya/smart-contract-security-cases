# M-5 - Zero-output exact-input swaps advance the price cursor

**Severity:** Medium (final Sherlock report)  
**Contracts:** `SwapMath.sol`, `MetricOmmPool.sol`  
**Category:** State-transition invariant, precision, LP sandwich  
**Original report:** [Metric Sherlock final PDF, pp. 35-46](https://github.com/Metricxyz/Known_issues/blob/main/sherlock/2026.09.15%20-%20Final%20-%20Metric%20Public%20Bug%20Bounty%20Audit%20Contest%20Report%201789468517.pdf)  
**Original finding referenced in report:** https://github.com/sherlock-audit/2026-07-metric-judging/issues/2419

## Root cause

In the exact-input functions `buyToken0InBinSpecifiedIn` and `buyToken1InBinSpecifiedIn`, a price-limit-constrained cursor movement can produce a token output that rounds down to zero. The input and fees become zero too, **but the function still returns the advanced cursor**, which the pool persists.

The resulting transition violates the intended relationship between the bin's cursor and reserves:

```text
before: cursor = X, reserves = (R0, R1)
after:  cursor = Y, reserves = (R0, R1), Y != X
paid = 0, received = 0, fee = 0
```

A previous safeguard for the **exact-output** functions does not cover these **exact-input** functions.

## Conditions

- The active bin initially has sufficiently thin liquidity so a small nonzero cursor step rounds to zero output.
- The public pool entrypoint can be called directly with a custom swap callback (even if a higher-level router rejects zero deltas).
- A victim subsequently adds exact-share liquidity against the unchanged reserves.
- The attacker can position transactions around that deposit.

## Exploit path

1. The attacker submits a series of zero-output exact-input swaps.
2. Each swap changes the active cursor at no token cost.
3. The victim's exact-share deposit uses the existing reserve proportions, unaware that the cursor is inconsistent with them.
4. The attacker trades through the artificial price interval and returns the cursor toward the honest midpoint.
5. The newly deposited LP capital absorbs the loss.

## Impact shown by the original report

The submitted PoC reports **347 zero-delta swap calls**, followed by approximately **$33.08 loss** on a **$99,899.99** victim position; attacker profit is nearly identical. The full path was reported to use about **8.56 million gas**.

## Reported remediation

For each exact-input direction, a zero token output should return the original cursor and zero accounting deltas before any storage update. The report links to [Metric-OMM/metric-core PR #63](https://github.com/Metric-OMM/metric-core/pull/63).

## Candidate verification property (not yet tested)

For any successful exact-input swap step, if both net token deltas are zero, the step must not mutate the active-bin cursor, reserves, fee accrual, or any related economic state. More generally, cursor movement must be consistently linked to an economically meaningful reserve transition.

This is an unusually attractive target for bytecode-level symbolic execution because it concerns a concrete relation between pre-state, post-state and observable token deltas.

## Attribution

This is a summary of a third-party published finding. See the Sherlock report for the original researchers, full PoC, discussion, and remediation details.
