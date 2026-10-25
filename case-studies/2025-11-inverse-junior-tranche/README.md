# Inverse Finance - Junior Tranche

- **Engagement:** [Sherlock contest #1202](https://audits.sherlock.xyz/contests/1202)
- **Date:** Nov 2025
- **Category:** Lending / ERC-4626
- **Source status:** Primary final report
- **Official report:** [Open report](https://www.inverse.finance/audits/junior-sherlock-contest.pdf)

## Selected case studies

| ID | Technical issue | Severity |
| --- | --- | --- |
| M-1 | [maxDeposit reports unlimited capacity despite actual restrictions](maxdeposit-erc4626-cap.md) | Medium |
| M-2 | [Exit-window equality lets renewal bypass the withdrawal fee](exit-window-boundary-fee.md) | Medium |

## Scope and attribution

These are annotated studies of published findings by other researchers, not personal audit credits. Severity is transcribed from the primary report when available; otherwise it is labelled as secondary. The verification angles are proposed proof obligations, not assertions that `pevm` found or proved the cases.
