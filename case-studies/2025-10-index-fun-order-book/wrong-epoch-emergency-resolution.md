# Emergency resolution targets the live epoch instead of the intended epoch

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Secondary disclosures; primary PDF not located.  
> **Reported severity:** Medium (secondary source).

## Root cause

Emergency resolver reads `currentEpoch` dynamically rather than accepting and checking the epoch to be resolved.

## Preconditions

Time-based market rolls over between closure of an old epoch and emergency resolution.

## Failure / attack path

Emergency call operates on a new trading epoch; the previous epoch remains unresolved and the new epoch can receive the wrong Merkle root.

## Reported impact

Blocked previous-epoch claims and incorrect state for a future epoch; secondary source reports a fix introducing an explicit epoch parameter.

## Suggested mitigation

Resolve an explicit eligible epoch, validate ordering and prevent finalisation of an active trading epoch.

## Verification angle (proposal, not a proved property)

An emergency settlement of epoch e may mutate settlement data for e only and must never settle a live epoch.

## Sources and attribution

- [Disclosed finding / source used](https://coinbuggie.com/protocols/index-fun-order-book)
- [Sherlock contest #1197](https://audits.sherlock.xyz/contests/1197)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
