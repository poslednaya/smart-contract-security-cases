# Incorrect integration of exponentially decaying borrowing interest

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Primary final report.  
> **Reported severity:** Medium.

## Root cause

A piecewise integral in `InterestModel.calculateInterest` incorrectly scales the decaying-rate contribution after a trajectory reaches the minimum rate.

## Preconditions

Initial rate exceeds the minimum and elapsed time is sufficient to cross down to the minimum.

## Failure / attack path

Accrual formula undercounts the exponential part while applying the floor-rate part, producing significantly less charged interest.

## Reported impact

Report example with 1,000,000 debt over 60 days estimates roughly 185 units charged versus 13,880 by the correct mathematical integration; the final table categorises it Medium despite language in issue text.

## Suggested mitigation

Repair fixed-point scaling in each integral segment and test the boundary where the decay crosses MIN_RATE.

## Verification angle (proposal, not a proved property)

Interest accrued over an interval must approximate the integral of the configured instantaneous interest rate with a documented bounded rounding error.

## Sources and attribution

- [Disclosed finding / source used](https://monolith-public-files.vercel.app/audits/Sherlock-Monolith-Public-Audit-Contest-Report-December-2025.pdf)
- [Sherlock contest #1212](https://audits.sherlock.xyz/contests/1212)
