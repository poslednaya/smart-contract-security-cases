# Uniswap V3 oracle fails when observation history is not initialized

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Secondary disclosure; complete official findings not publicly accessible.  
> **Reported severity:** Medium (secondary source).

## Root cause

`StNxmOracle` references a Uniswap V3 pool for a 30-minute TWAP but does not ensure sufficient observation cardinality/history exists.

## Preconditions

A newly initialized pool has inadequate observation history (e.g. default cardinality of one).

## Failure / attack path

`OracleLibrary.consult` requests historical TWAP data and reverts, so the dependent `price()` read reverts too.

## Reported impact

Oracle and dependent integrations cannot use price data until the observation buffer is increased and sufficiently populated; secondary source reports remediation.

## Suggested mitigation

Increase observation cardinality during setup and guard price reads until the required observation horizon is actually populated.

## Verification angle (proposal, not a proved property)

Oracle consumption is permitted only if the underlying observation history covers the lookback interval, otherwise fail in a documented controlled manner.

## Sources and attribution

- [Disclosed finding / source used](https://coinbuggie.com/vulnerabilities/oracle-manipulation)
- [Sherlock contest #1203](https://audits.sherlock.xyz/contests/1203)

**Limitation:** This note relies on public secondary descriptions. Check the original final PDF / judge decision before treating all details, severity labels, and fixes as independently verified.
