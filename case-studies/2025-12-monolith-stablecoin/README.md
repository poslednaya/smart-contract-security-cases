# Monolith Stablecoin Factory

- **Engagement:** [Sherlock contest #1212](https://audits.sherlock.xyz/contests/1212)
- **Date:** Dec 2025
- **Category:** Stablecoin / Lending
- **Source status:** Primary final report
- **Official report:** [Open report](https://monolith-public-files.vercel.app/audits/Sherlock-Monolith-Public-Audit-Contest-Report-December-2025.pdf)

## Selected case studies

| ID | Technical issue | Severity |
| --- | --- | --- |
| H-1 | [Free-debt share inflation permits unbacked borrowing](free-debt-share-inflation.md) | High |
| M-1 | [Bad-debt write-off can be recycled into repeated unbacked issuance](bad-debt-writeoff-loop.md) | Medium |
| M-2 | [Health-factor equality disagrees between borrow and liquidation](liquidation-health-boundary.md) | Medium |
| M-5 | [Incorrect integration of exponentially decaying borrowing interest](interest-integral-scale-error.md) | Medium |

## Scope and attribution

These are annotated studies of published findings by other researchers, not personal audit credits. Severity is transcribed from the primary report when available; otherwise it is labelled as secondary. The verification angles are proposed proof obligations, not assertions that `pevm` found or proved the cases.
