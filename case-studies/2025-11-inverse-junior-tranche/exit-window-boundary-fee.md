# Exit-window equality lets renewal bypass the withdrawal fee

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Primary final report.  
> **Reported severity:** Medium.

## Root cause

`WithdrawalEscrow.queueWithdrawal` uses `block.timestamp > exitWindowStart` instead of `>=`, sending the equality case down the lower-fee path.

## Preconditions

A queued withdrawal is renewed precisely at `exitWindowStart`; fee is nonzero.

## Failure / attack path

At the boundary timestamp the renewal charges a fee only on newly queued assets, potentially zero, rather than the entire pending position.

## Reported impact

Avoidance of the full withdrawal fee and lost fee revenue for the vault; the primary report provides illustrative amounts.

## Suggested mitigation

Apply full fee once `block.timestamp >= exitWindowStart`; add boundary tests at t-1, t, t+1.

## Verification angle (proposal, not a proved property)

At and after the exit-window start, any renewal must charge the defined full fee on the appropriate outstanding withdrawal base.

## Sources and attribution

- [Disclosed finding / source used](https://www.inverse.finance/audits/junior-sherlock-contest.pdf)
- [Sherlock contest #1202](https://audits.sherlock.xyz/contests/1202)
