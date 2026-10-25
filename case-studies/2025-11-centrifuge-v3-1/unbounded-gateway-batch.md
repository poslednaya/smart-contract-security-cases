# Unbounded cross-chain batch message count can trigger DoS

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Official report location confirmed; selected mechanisms corroborated via secondary disclosures.  
> **Reported severity:** Medium (secondary source).

## Root cause

`Gateway.withBatch()` does not cap the number of accumulated messages before downstream processing.

## Preconditions

Caller can assemble a batch large enough to exceed practical execution/message limits.

## Failure / attack path

Batch aggregation and subsequent processing face a gas or size failure that may obstruct otherwise valid cross-chain messages.

## Reported impact

The secondary disclosure flags potential persistent denial of service; full protocol-specific reachability was not independently checked.

## Suggested mitigation

Bound the number and byte size of messages, and make batch processing resumable or reject oversized batches before state commitment.

## Verification angle (proposal, not a proved property)

Any accepted batch can be fully processed under the protocol's stated resource bounds; batch size never exceeds validated limits.

## Sources and attribution

- [Disclosed finding / source used](https://coinbuggie.com/vulnerabilities/bridge-exploit)
- [Sherlock contest #1028](https://audits.sherlock.xyz/contests/1028)
- [Official final report](https://github.com/centrifuge/protocol/blob/main/docs/audits/2025-12-Sherlock-Blackthorn.pdf)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
