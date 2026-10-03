# Executive Risk Memo

**To:** Simulated application sponsor and business risk owner  
**From:** Ron Richardson  
**Date:** October 3, 2026  
**Subject:** Prioritize access control and exposure reduction before routine hardening

## Recommendation

Approve a validation-first remediation plan. Investigate the potential remote file inclusion flag before concluding that the application can be compromised. In parallel, determine whether anonymous FTP access is necessary and whether it exposes sensitive files. These two decisions should precede the remaining hardening work because they concern possible application control and unauthenticated access to data.

## Why this matters to the business

For this exercise, the application is assumed to support internal work and potentially hold sensitive files. If remote inclusion is executable, an attacker could gain control of application behavior. If anonymous access exposes sensitive content, confidentiality could be lost without a named user account. Neither outcome has been demonstrated. Actual data sensitivity and business dependency must be established before management can quantify impact or approve a lasting exception.

The remaining observations concern excessive diagnostic information, session protection and configuration hardening. Addressing them reduces opportunities for reconnaissance or compound attacks. Their scanner presence alone does not demonstrate a breach.

## Decisions requested

1. Nominate a business risk owner and confirm the application's data classification and operational importance.
2. Approve the proposed technical owners and dates in the [POA&M](Project_1_Vulnerability_Risk_POAM.xlsx), with early validation of the possible inclusion issue and review of anonymous access.
3. Authorize required validation within the lab's permitted scope and decide whether any service exposure is justified by business need.

No remediation budget or loss estimate is presented: implementation effort, exposure and data value have not been established.

## Accountability and reporting

Use the POA&M for weekly progress review. Technical owners supply implementation and retest evidence; the risk owner approves exceptions and assesses residual risk. Any acceptance must record the rationale, compensating controls, approver and review date. Report validated, implemented and closed items separately so activity is not mistaken for demonstrated risk reduction.

**Current position:** nine observations tracked; zero closed. This is a simulated management assessment based on mixed teaching and user evidence. Detailed analysis belongs in [FINDINGS.md](FINDINGS.md); source limitations belong in the [evidence register](evidence/README.md).
