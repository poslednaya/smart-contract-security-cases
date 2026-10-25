# ETH attached to a batched bridge call becomes stranded

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Official report location confirmed; selected mechanisms corroborated via secondary disclosures.  
> **Reported severity:** Medium (secondary source).

## Root cause

`VaultRouter.crosschainTransferShares` accepts `msg.value`, while the batching route resets the forwarded amount to zero and neither refunds nor attributes the value.

## Preconditions

User calls the payable share bridge path with nonzero value while gateway batching is active.

## Failure / attack path

The transfer occurs in the batch-funded mode; the user's attached ETH remains in router custody.

## Reported impact

Repeatable unintended ETH retention; secondary disclosure describes a remediation that rejects ETH attached during batching.

## Suggested mitigation

Revert on `msg.value > 0` while batching, or explicitly refund it atomically.

## Verification angle (proposal, not a proved property)

For any successful route receiving msg.value, each wei is either transferred to its documented destination, refunded, or recorded as an attributed balance.

## Sources and attribution

- [Disclosed finding / source used](https://coinbuggie.com/vulnerabilities/bridge-exploit)
- [Sherlock contest #1028](https://audits.sherlock.xyz/contests/1028)
- [Official final report](https://github.com/centrifuge/protocol/blob/main/docs/audits/2025-12-Sherlock-Blackthorn.pdf)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
