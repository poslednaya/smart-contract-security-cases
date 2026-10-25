# maxDeposit reports unlimited capacity despite actual restrictions

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Primary final report.  
> **Reported severity:** Medium.

## Root cause

`jDola` inherits Solmate's default `maxDeposit()` which returns `type(uint256).max`, while `afterDeposit()` enforces share and asset limits.

## Preconditions

Vault approaches or reaches the share/asset cap or other enforced deposit constraint.

## Failure / attack path

An ERC-4626 integrator queries `maxDeposit()` and sends an amount deemed allowed; deposit then reverts at the vault-specific limit check.

## Reported impact

Breaks ERC-4626 maxDeposit requirements and can fail integrations; no fund-theft claim in the primary report.

## Suggested mitigation

Override `maxDeposit` to conservatively reflect all enforced caps and conversion rounding; the report cites InverseFinance/JuniorDola#11.

## Verification angle (proposal, not a proved property)

For every receiver and amount a <= maxDeposit(receiver), a deposit of a must not revert due to the vault's own capacity/share caps (separate allowances and balances from this condition).

## Sources and attribution

- [Disclosed finding / source used](https://www.inverse.finance/audits/junior-sherlock-contest.pdf)
- [Sherlock contest #1202](https://audits.sherlock.xyz/contests/1202)
