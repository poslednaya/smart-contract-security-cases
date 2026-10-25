# Health-factor equality disagrees between borrow and liquidation

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Primary final report.  
> **Reported severity:** Medium.

## Root cause

`adjust()` and `getLiquidatableDebt()` handle equality at the borrowing-power boundary differently (`>=` versus a stricter test).

## Preconditions

Borrower's debt equals borrowing power precisely.

## Failure / attack path

Position passes an adjustment health check but is simultaneously considered liquidatable.

## Reported impact

Incorrect liquidation eligibility at the boundary according to the primary report.

## Suggested mitigation

Centralise the health calculation and use consistent boundary comparisons for borrow and liquidation eligibility.

## Verification angle (proposal, not a proved property)

Every position accepted as healthy at transaction end must not be immediately liquidatable without any exogenous state change.

## Sources and attribution

- [Disclosed finding / source used](https://monolith-public-files.vercel.app/audits/Sherlock-Monolith-Public-Audit-Contest-Report-December-2025.pdf)
- [Sherlock contest #1212](https://audits.sherlock.xyz/contests/1212)
