# Smart Contract Security Case Studies

Technical notes on publicly disclosed smart contract vulnerabilities, with an emphasis on EVM execution, accounting, precision, invariants, and verification opportunities.

> **Attribution:** These are analyses of findings published by other security researchers. They are **not my original audit discoveries** unless explicitly marked otherwise. The original authors and sources are credited through the referenced reports. Described PoC results are taken from the original reports; I have not independently reproduced them.

## Projects

| Date | Protocol | Category | Chain | Cases analyzed | Original audit |
| --- | --- | --- | --- | --- | --- |
| Jul 2026 | [Metric OMM](case-studies/2026-07-metric-omm/README.md) | Oracle-based DEX / AMM | EVM | [5 Medium](case-studies/2026-07-metric-omm/README.md#selected-case-studies) | [Sherlock #1279](https://audits.sherlock.xyz/contests/1279) |

## Methodology

For each published finding, these notes summarize:

1. The affected contract and the root cause.
2. The necessary preconditions and the failure or attack path.
3. The observed or claimed impact, **as reported** by the original researchers.
4. The reported mitigation / remediation reference.
5. A possible verification property or invariant to investigate.

**Verification properties are research ideas, not claims that a formal prover has already established or detected the vulnerability.** Final severity is reproduced from the audit report, even when a finding's text discusses a higher severity.

A reusable outline for future projects is available at [templates/case-study-template.md](templates/case-study-template.md).
