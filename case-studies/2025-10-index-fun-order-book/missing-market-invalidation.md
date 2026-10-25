# No emergency invalidation path for unresolved markets

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Secondary disclosures; primary PDF not located.  
> **Reported severity:** Medium (secondary source).

## Root cause

Settlement and withdrawal routes require a valid Merkle resolution root; no explicit cancellation/invalidation route exists for a permanently unresolved market.

## Preconditions

Underlying event is cancelled or becomes unresolvable, or the resolution source cannot issue an accepted root.

## Failure / attack path

Users deposited collateral but cannot produce a resolution proof; claims continue to revert and no emergency refund path is available.

## Reported impact

Locked market collateral in the unresolvable-event scenario, as described by secondary disclosure.

## Suggested mitigation

Specify and implement a bounded, privileged or time-locked invalidation/refund flow with safeguards against malicious cancellation.

## Verification angle (proposal, not a proved property)

Every market must eventually admit either a valid resolution/claim or a safely authorised cancellation/refund transition.

## Sources and attribution

- [Disclosed finding / source used](https://coinbuggie.com/protocols/index-fun-order-book)
- [Sherlock contest #1197](https://audits.sherlock.xyz/contests/1197)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
