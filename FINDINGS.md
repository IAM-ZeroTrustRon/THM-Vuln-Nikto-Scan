# Findings Analysis

This document explains the evidence and risk reasoning behind each POA&M entry. It does not assign new CVSS scores. P1/P2/P3 are planning priorities, based on assumed business consequences and uncertainty. Owners, dates, status and closure requirements are maintained in the [POA&M workbook](Project_1_Vulnerability_Risk_POAM.xlsx). Evidence IDs resolve through the [evidence register](evidence/README.md).

## F01 — Potential remote file inclusion: file parameter

**Evidence basis:** E01: Nikto flag; exploitation unverified.

**Observation:** A file parameter was flagged by Nikto as a possible remote inclusion path. This is a test result requiring investigation, not proof that remote content was executed.

**Control objective:** Application input handling should prevent user-controlled values from selecting arbitrary code or remote resources.

**Business consequence:** If executable remote inclusion is confirmed: application compromise and data exposure.

**Validation questions:** Which code consumes the parameter? Can it reach an inclusion operation? Are remote resources permitted by application and runtime configuration?

**Priority rationale (P1):** Potential compromise justifies early validation even without a scanner score. If validation disproves inclusion, record the basis rather than treating the flag as a remediated vulnerability.

**Recommended treatment:** Validate safely in authorized lab; remove remote inclusion; allowlist local identifiers.

## F02 — Anonymous FTP login

**Evidence basis:** E02: published OpenVAS report.

**Observation:** The published OpenVAS reference reports anonymous FTP login with severity 6.4 and CVE-1999-0497. This is platform reference evidence, not a retained original scan export.

**Control objective:** File access should require authorized identity unless an explicit public-distribution use case has been approved.

**Business consequence:** Unauthorized access to files if sensitive content is exposed; write access not established.

**Validation questions:** What can an anonymous session read? Is any write operation permitted? Are the files intended to be public, and is FTP required?

**Priority rationale (P1):** The central GRC decision is whether unauthenticated access has an approved business purpose. Login alone does not prove sensitive-file exposure or write access.

**Recommended treatment:** Disable anonymous login unless approved; inventory exposed files; restrict access.

## F03 — Exposed phpinfo page: /info.php

**Evidence basis:** E01/E02/E03: scanner output and screenshot.

**Observation:** Nikto and the OpenVAS reference identify a phpinfo diagnostic page; the user screenshot corroborates the reported 5.3 severity answer.

**Control objective:** Diagnostic interfaces should be removed from ordinary deployment or restricted to authorized administrators.

**Business consequence:** System details may help attackers identify exploitable components.

**Validation questions:** Is the endpoint accessible without authentication? Which configuration details are disclosed? Is it part of a deployment artifact?

**Priority rationale (P2):** Treat the disclosure as reconnaissance support. Generic CVEs listed by a detection test do not establish that every referenced product is installed or vulnerable.

**Recommended treatment:** Remove diagnostic page from deployment; deny public access.

## F04 — PHPSESSID cookie lacks HttpOnly

**Evidence basis:** E01: Nikto output.

**Observation:** The Nikto excerpt reports a PHPSESSID cookie without HttpOnly.

**Control objective:** Browser-access restrictions on session cookies should reduce the consequences of script execution.

**Business consequence:** Session cookie theft could worsen impact of a separate script-injection weakness.

**Validation questions:** Which response sets the cookie? Is the attribute consistently absent? What session workflow could a change affect?

**Priority rationale (P2):** The business consequence depends on a separate script-injection path. HttpOnly is a session safeguard, not a fix for cross-site scripting; Secure and SameSite need their own assessment.

**Recommended treatment:** Set HttpOnly on session cookies; review Secure and SameSite separately.

## F05 — Directory listing enabled: /static/

**Evidence basis:** E01: Nikto output.

**Observation:** Nikto reports a directory listing at /static/. The excerpt does not inventory the listed content.

**Control objective:** Published directories should expose only approved files, without unnecessary discovery of deployment contents.

**Business consequence:** Unintended file discovery may expose internal content.

**Validation questions:** Which files are listed? Are backups, source, metadata or sensitive material present? Do approved static assets require directory browsing?

**Priority rationale (P2):** The risk rises with the content exposed. Do not infer a secret leak solely from a listing; content review determines the confidentiality consequence.

**Recommended treatment:** Disable indexing; review content for secrets or unintended files.

## F06 — Apache /server-status exposed

**Evidence basis:** E01: Nikto output.

**Observation:** The excerpt reports an accessible Apache /server-status endpoint. The captured excerpt does not show its detailed response.

**Control objective:** Operational telemetry should be limited to authorized management or monitoring access.

**Business consequence:** Operational details may support reconnaissance.

**Validation questions:** Is access unauthenticated? What information is returned? Which monitoring process legitimately needs it?

**Priority rationale (P2):** Restriction should preserve authorized monitoring. The business concern is operational information exposure rather than demonstrated loss of application control.

**Recommended treatment:** Restrict status endpoint to authorized management access.

## F07 — Clickjacking protection header absent

**Evidence basis:** E01: Nikto output; CSP not checked.

**Observation:** Nikto reports missing X-Frame-Options. No captured evidence establishes the presence or absence of a suitable CSP frame-ancestors policy.

**Control objective:** Sensitive user actions should be protected from unauthorized embedding in another site.

**Business consequence:** Sensitive actions could be exposed to UI deception if no equivalent protection exists.

**Validation questions:** Does CSP already restrict framing? Which actions are sensitive? Are any embedded workflows explicitly required?

**Priority rationale (P3):** An absent header is insufficient to conclude exploitable clickjacking. Evaluate equivalent protection and business integration requirements before prescribing a change.

**Recommended treatment:** Check CSP frame-ancestors; configure appropriate framing restriction.

## F08 — DEBUG HTTP method flagged

**Evidence basis:** E01: Nikto flag; behavior unverified.

**Observation:** Nikto flags the DEBUG method as potentially exposing diagnostic information. No request/response transcript verifies that behavior.

**Control objective:** Unnecessary diagnostic behavior should be disabled on application-facing services.

**Business consequence:** Debug information disclosure if method actually exposes details.

**Validation questions:** What status and response body does the method return? Does it reveal diagnostic content beyond normal responses?

**Priority rationale (P3):** Validate actual behavior before allocating remediation effort or claiming a confirmed disclosure. A scanner flag is an investigation input.

**Recommended treatment:** Validate method response; disable unnecessary debug behavior.

## F09 — ICMP timestamp information disclosure

**Evidence basis:** E02: published OpenVAS report.

**Observation:** The published OpenVAS reference reports ICMP timestamp disclosure at severity 2.1 and CVE-1999-0524.

**Control objective:** Network responses should disclose only information needed for approved operations.

**Business consequence:** Limited reconnaissance information; lower priority than access and data exposure.

**Validation questions:** Does the host answer timestamp requests? What filtering is feasible without disturbing required network functions?

**Priority rationale (P3):** Prioritize access and potentially sensitive content before this lower-impact reconnaissance observation. Operational requirements inform the hardening decision.

**Recommended treatment:** Restrict timestamp responses where operationally appropriate.
