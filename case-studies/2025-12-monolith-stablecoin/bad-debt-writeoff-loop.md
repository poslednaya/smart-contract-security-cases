# Bad-debt write-off can be recycled into repeated unbacked issuance

> **Provenance:** Independent analysis of a published finding. Not an original discovery or an independently reproduced exploit.  
> **Source confidence:** Primary final report.  
> **Reported severity:** Medium.

## Root cause

`writeOff` redistributes the borrower's debt across remaining debt pools while transferring that borrower's residual collateral to a caller-supplied recipient.

## Preconditions

Bad-debt borrower is the only borrower in one category, or the attacker can manipulate the remaining borrower distribution.

## Failure / attack path

An attacker rotates positions and calls write-off repeatedly so collateral is returned while liability is shifted to another controlled position.

## Reported impact

The primary report presents a repeatable way to mint unbacked tokens; final severity Medium. Sponsor PR #42 listed.

## Suggested mitigation

Do not allow a write-off to return meaningful collateral to an adversarial recipient while socialising the associated debt; preserve debt conservation.

## Verification angle (proposal, not a proved property)

A write-off cannot increase a coalition's net claimable collateral + issued coins beyond its pre-write-off net value.

## Sources and attribution

- [Disclosed finding / source used](https://monolith-public-files.vercel.app/audits/Sherlock-Monolith-Public-Audit-Contest-Report-December-2025.pdf)
- [Sherlock contest #1212](https://audits.sherlock.xyz/contests/1212)
