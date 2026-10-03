# Findings and risk governance

This is a training-based GRC assessment, not a production penetration test. Nine observations are tracked in the POA&M; scanner detection does not establish exploitation, a breach or regulatory noncompliance. The business scenario assumes an internal application with potentially sensitive files. Actual exposure and data sensitivity are unknown.

| ID | Observation | GRC priority and business concern | Proposed accountable function |
|---|---|---|---|
| F01 | Potential remote file inclusion | P1: validate promptly; application compromise is conditional, not proven | Application Engineering |
| F02 | Anonymous FTP login | P1: determine whether unauthenticated access exposes sensitive files | Infrastructure Operations |
| F03 | Exposed phpinfo page | P2: reduce information available for reconnaissance | Application Engineering |
| F04 | Session cookie lacks HttpOnly | P2: limit session impact if a separate script-injection weakness exists | Application Engineering |
| F05 | Directory indexing | P2: prevent unintended file discovery and review published content | Web Operations |
| F06 | Exposed server-status | P2: restrict operational information to authorized monitoring | Web Operations |
| F07 | Missing framing header | P3: verify equivalent CSP protection before concluding exploitable clickjacking | Application Engineering |
| F08 | DEBUG method flag | P3: validate actual disclosure before treating the flag as a confirmed weakness | Web Operations |
| F09 | ICMP timestamp response | P3: address lower-impact reconnaissance subject to operational requirements | Network Operations |

## Management decision and oversight

Approve a validation-first sequence and nominate owners. Proposed dates are October 5 for F01, October 10 for F02, October 17 for P2 items and November 2 for P3 items, all in 2026. These dates are planning proposals, not approved service-level commitments. P1/P2/P3 reflect analyst judgment about assumed business impact and evidence confidence; they are separate from scanner severity.

Review progress weekly after owner approval. Track validation, implementation and closure separately. Escalate missed approved dates to the designated risk owner. An exception requires an approver, business rationale, compensating controls and review date; it does not count as remediation.

Close a finding only with configuration evidence, an authorized retest and a functionality check. Residual risk remains unvalidated until that evidence is reviewed. No fixes, risk reduction, production experience or regulatory compliance are claimed.

## Evidence limits

Nikto evidence has inconsistent IP/hostname values and is preserved as a historical excerpt. OpenVAS images are platform teaching references, not original user scan exports. The user's completion screenshot demonstrates room completion, not implemented remediation. The supplemental `nmap -A 127.0.0.1` screenshot shows a partial aggressive scan of the AttackBox itself and adds no findings to the assessed target. See [evidence register](evidence/README.md) and the POA&M for confidence, dates and closure criteria.
