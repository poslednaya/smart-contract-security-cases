# Uncapped withdrawal forwarded to the liquidity layer

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Secondary disclosure; official contest source.  
> **Reported severity:** High.

## Root cause

The money-market `_processNormalSupplyAction` constrains the accounting quantity to the user's supply but passes the original, larger requested withdrawal to `LIQUIDITY.operate`.

## Preconditions

A user can enter the normal supply path with a small supplied position and request a withdrawal larger than that position.

## Failure / attack path

The helper caps the position delta and clears position accounting as if the permitted balance was withdrawn; downstream liquidity transfer uses the unbounded requested amount.

## Reported impact

Secondary disclosure describes direct extraction of protocol funds in excess of the user's supplied balance; it identifies the finding as Sherlock High.

## Suggested mitigation

Use the same validated/capped withdrawal quantity for the position update and liquidity transfer. Reject over-withdrawal if the specification requires exact amounts.

## Verification angle (proposal, not a proved property)

For every successful withdrawal, transferred assets must not exceed the assets debited from the caller's position, subject to explicitly modelled yield/fees.

## Sources and attribution

- [Disclosed finding / source used](https://coinbuggie.com/reports/f29eac7a-38f8-4270-b874-4842af8b8435)
- [Sherlock contest #1225](https://audits.sherlock.xyz/contests/1225)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
