# Seller is charged the buyer's trade fee

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Secondary disclosures; primary PDF not located.  
> **Reported severity:** High.

## Root cause

In `_executeTokenSwap` / `_executeAgainstMatcher`, the buyer-side trade fee is deducted from seller proceeds rather than charged on top of the buyer's cost.

## Preconditions

An order is filled via the token-swap settlement path with a nonzero effective buyer fee.

## Failure / attack path

Trade settles, but the seller receives the agreed consideration minus a fee that contract economics assign to the buyer.

## Reported impact

Systematic reduction of seller and market-maker proceeds; publicly disclosed as High and reported fixed by the sponsor.

## Suggested mitigation

Separate buyer fee collection from seller payout and assert exact conservation of settlement amounts.

## Verification angle (proposal, not a proved property)

For any valid fill, seller proceeds >= agreed price minus only explicitly seller-borne fees; buyer-borne fees cannot reduce this amount.

## Sources and attribution

- [Disclosed finding / source used](https://coinbuggie.com/protocols/index-fun-order-book)
- [Sherlock contest #1197](https://audits.sherlock.xyz/contests/1197)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
