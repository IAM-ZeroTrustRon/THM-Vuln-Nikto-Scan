# Findings Analysis

This is the authoritative audit-style findings record for F01–F09. It distinguishes scanner observations and teaching references from verified control effectiveness. Criteria below are proposed assessment benchmarks, not an adopted organizational policy or a finding of legal noncompliance.

This document explains the evidence and risk reasoning behind each POA&M entry. It does not assign new CVSS scores. P1/P2/P3 are planning priorities, based on assumed business consequences and uncertainty. Owners, dates, status and closure requirements are maintained in the [POA&M workbook](../Project_1_Vulnerability_Risk_POAM.xlsx). Evidence IDs resolve through the [evidence register](../evidence/README.md).

## F01 — Potential remote file inclusion: file parameter

**Evidence / assurance status:** E01: Nikto flag; exploitation unverified.

**Condition:** A file parameter was flagged by Nikto as a possible remote inclusion path. This is a test result requiring investigation, not proof that remote content was executed.

**Criteria — proposed assessment benchmark:** Application input handling should prevent user-controlled values from selecting arbitrary code or remote resources.

**Impact (business risk):** If executable remote inclusion is confirmed: application compromise and data exposure.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** Which code consumes the parameter? Can it reach an inclusion operation? Are remote resources permitted by application and runtime configuration?

**Priority rationale (P1):** Potential compromise justifies early validation even without a scanner score. If validation disproves inclusion, record the basis rather than treating the flag as a remediated vulnerability.

**Recommendation:** Validate safely in authorized lab; remove remote inclusion; allowlist local identifiers.

## F02 — Anonymous FTP login

**Evidence / assurance status:** E02: published OpenVAS report.

**Condition:** The published OpenVAS reference reports anonymous FTP login with severity 6.4 and CVE-1999-0497. This is platform reference evidence, not a retained original scan export.

**Criteria — proposed assessment benchmark:** File access should require authorized identity unless an explicit public-distribution use case has been approved.

**Impact (business risk):** Unauthorized access to files if sensitive content is exposed; write access not established.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** What can an anonymous session read? Is any write operation permitted? Are the files intended to be public, and is FTP required?

**Priority rationale (P1):** The central GRC decision is whether unauthenticated access has an approved business purpose. Login alone does not prove sensitive-file exposure or write access.

**Recommendation:** Disable anonymous login unless approved; inventory exposed files; restrict access.

## F03 — Exposed phpinfo page: /info.php

**Evidence / assurance status:** E01/E02/E03: scanner output and screenshot.

**Condition:** Nikto and the OpenVAS reference identify a phpinfo diagnostic page; the user screenshot corroborates the reported 5.3 severity answer.

**Criteria — proposed assessment benchmark:** Diagnostic interfaces should be removed from ordinary deployment or restricted to authorized administrators.

**Impact (business risk):** System details may help attackers identify exploitable components.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** Is the endpoint accessible without authentication? Which configuration details are disclosed? Is it part of a deployment artifact?

**Priority rationale (P2):** Treat the disclosure as reconnaissance support. Generic CVEs listed by a detection test do not establish that every referenced product is installed or vulnerable.

**Recommendation:** Remove diagnostic page from deployment; deny public access.

## F04 — PHPSESSID cookie lacks HttpOnly

**Evidence / assurance status:** E01: Nikto output.

**Condition:** The Nikto excerpt reports a PHPSESSID cookie without HttpOnly.

**Criteria — proposed assessment benchmark:** Browser-access restrictions on session cookies should reduce the consequences of script execution.

**Impact (business risk):** Session cookie theft could worsen impact of a separate script-injection weakness.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** Which response sets the cookie? Is the attribute consistently absent? What session workflow could a change affect?

**Priority rationale (P2):** The business consequence depends on a separate script-injection path. HttpOnly is a session safeguard, not a fix for cross-site scripting; Secure and SameSite need their own assessment.

**Recommendation:** Set HttpOnly on session cookies; review Secure and SameSite separately.

## F05 — Directory listing enabled: /static/

**Evidence / assurance status:** E01: Nikto output.

**Condition:** Nikto reports a directory listing at /static/. The excerpt does not inventory the listed content.

**Criteria — proposed assessment benchmark:** Published directories should expose only approved files, without unnecessary discovery of deployment contents.

**Impact (business risk):** Unintended file discovery may expose internal content.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** Which files are listed? Are backups, source, metadata or sensitive material present? Do approved static assets require directory browsing?

**Priority rationale (P2):** The risk rises with the content exposed. Do not infer a secret leak solely from a listing; content review determines the confidentiality consequence.

**Recommendation:** Disable indexing; review content for secrets or unintended files.

## F06 — Apache /server-status exposed

**Evidence / assurance status:** E01: Nikto output.

**Condition:** The excerpt reports an accessible Apache /server-status endpoint. The captured excerpt does not show its detailed response.

**Criteria — proposed assessment benchmark:** Operational telemetry should be limited to authorized management or monitoring access.

**Impact (business risk):** Operational details may support reconnaissance.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** Is access unauthenticated? What information is returned? Which monitoring process legitimately needs it?

**Priority rationale (P2):** Restriction should preserve authorized monitoring. The business concern is operational information exposure rather than demonstrated loss of application control.

**Recommendation:** Restrict status endpoint to authorized management access.

## F07 — Clickjacking protection header absent

**Evidence / assurance status:** E01: Nikto output; CSP not checked.

**Condition:** Nikto reports missing X-Frame-Options. No captured evidence establishes the presence or absence of a suitable CSP frame-ancestors policy.

**Criteria — proposed assessment benchmark:** Sensitive user actions should be protected from unauthorized embedding in another site.

**Impact (business risk):** Sensitive actions could be exposed to UI deception if no equivalent protection exists.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** Does CSP already restrict framing? Which actions are sensitive? Are any embedded workflows explicitly required?

**Priority rationale (P3):** An absent header is insufficient to conclude exploitable clickjacking. Evaluate equivalent protection and business integration requirements before prescribing a change.

**Recommendation:** Check CSP frame-ancestors; configure appropriate framing restriction.

## F08 — DEBUG HTTP method flagged

**Evidence / assurance status:** E01: Nikto flag; behavior unverified.

**Condition:** Nikto flags the DEBUG method as potentially exposing diagnostic information. No request/response transcript verifies that behavior.

**Criteria — proposed assessment benchmark:** Unnecessary diagnostic behavior should be disabled on application-facing services.

**Impact (business risk):** Debug information disclosure if method actually exposes details.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** What status and response body does the method return? Does it reveal diagnostic content beyond normal responses?

**Priority rationale (P3):** Validate actual behavior before allocating remediation effort or claiming a confirmed disclosure. A scanner flag is an investigation input.

**Recommendation:** Validate method response; disable unnecessary debug behavior.

## F09 — ICMP timestamp information disclosure

**Evidence / assurance status:** E02: published OpenVAS report.

**Condition:** The published OpenVAS reference reports ICMP timestamp disclosure at severity 2.1 and CVE-1999-0524.

**Criteria — proposed assessment benchmark:** Network responses should disclose only information needed for approved operations.

**Impact (business risk):** Limited reconnaissance information; lower priority than access and data exposure.

**Cause:** Not established by the retained evidence. Configuration, code and change records are needed; no organizational root cause is asserted.

**Validation questions:** Does the host answer timestamp requests? What filtering is feasible without disturbing required network functions?

**Priority rationale (P3):** Prioritize access and potentially sensitive content before this lower-impact reconnaissance observation. Operational requirements inform the hardening decision.

**Recommendation:** Restrict timestamp responses where operationally appropriate.

## Treatment ownership and closure

The POA&M is the authoritative action record for F01–F09: proposed owners, target dates, status and closure tests. Targets are proposals anchored to October 3, 2026, not accepted SLAs. Current residual risk is unassessed. No cause, compromise or remediation is inferred from scanner output alone.

## Framework alignment

| Review area | Framework outcome | Interpretation |
|---|---|---|
| Configuration exposure and unnecessary interfaces | NIST CSF 2.0 PR.PS-01 | Configuration management; relevance does not establish conformity |
| Vulnerability treatment | NIST CSF 2.0 PR.PS-02; CIS Control 7 | Risk-based maintenance and vulnerability management; no claim that this lab proves an operating enterprise program |
| Assessment and prioritization | NIST CSF 2.0 ID.RA | Identify, assess and prioritize risk using evidence and uncertainty |

Sources: [NIST CSF 2.0 Core](https://www.nist.gov/system/files/documents/2024/03/25/The_NIST_CSF_2-0_Core_With_Withdrawn_CSF_1-1_Elements.pdf), [CIS Control 7](https://www.cisecurity.org/controls/continuous-vulnerability-management). PR.IP identifiers belong to the earlier framework, not CSF 2.0. This general training lab does not establish HIPAA scope.
