# Free-debt share inflation permits unbacked borrowing

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Primary final report.  
> **Reported severity:** High.

## Root cause

Under certain redemption/rounding sequences, aggregate `totalFreeDebt` can become zero while `totalFreeDebtShares` remains extremely large; `increaseDebt` then mints shares 1:1 in its `totalFreeDebt == 0` branch.

## Preconditions

Attacker creates highly inflated debt shares across positions and drives aggregate free debt to zero without clearing all shares.

## Failure / attack path

Subsequent borrowing uses an inconsistent share conversion, so newly created shares represent much less debt than the issued stablecoins.

## Reported impact

The primary report demonstrates unbacked borrowing and cites a PoC; formally rated High in the final report (not a claim of an actual mainnet exploit).

## Suggested mitigation

Maintain coherent debt/share zero-state transitions, prevent orphan debt shares, and enforce backing on every debt issuance; sponsor fix PR MonolithMarket/Monolith#42.

## Verification angle (proposal, not a proved property)

If totalFreeDebt == 0, totalFreeDebtShares must also be zero (unless a formally justified state exists); debt issued must be fully represented in recoverable borrower liability.

## Sources and attribution

- [Disclosed finding / source used](https://monolith-public-files.vercel.app/audits/Sherlock-Monolith-Public-Audit-Contest-Report-December-2025.pdf)
- [Sherlock contest #1212](https://audits.sherlock.xyz/contests/1212)
