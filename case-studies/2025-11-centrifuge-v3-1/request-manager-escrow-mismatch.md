# Mutable request manager may redirect pending deposits across pools

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Official report location confirmed; selected mechanisms corroborated via secondary disclosures.  
> **Reported severity:** High (secondary source).

## Root cause

`Spoke.requestCallback` consults the current `requestManager` without tying the callback authority to the manager that originated a given pending request.

## Preconditions

Pending requests hold deposits in a shared escrow while a pool's request-manager configuration can change.

## Failure / attack path

The manager identity used on callback is no longer bound to the origin of escrowed assets, potentially enabling transfers between pool escrows.

## Reported impact

Secondary write-up characterises this as a High-risk theft of other pools' pending deposits; no independent reproduction here.

## Suggested mitigation

Bind each pending request to its originating pool and manager and validate the binding on callback and escrow transfer.

## Verification angle (proposal, not a proved property)

Assets escrowed for pool P and request R can be released only through transitions authorised for the stored (P,R,manager) identity.

## Sources and attribution

- [Disclosed finding / source used](https://crypto.training/hacks/64195-h-1-pool-managers-can-steal-all-other-pools-pending-deposits/)
- [Sherlock contest #1028](https://audits.sherlock.xyz/contests/1028)
- [Official final report](https://github.com/centrifuge/protocol/blob/main/docs/audits/2025-12-Sherlock-Blackthorn.pdf)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
