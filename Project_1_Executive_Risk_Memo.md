# Executive Risk Memo
**Project:** Vulnerability Risk & Remediation Assessment  
**Date:** October 3, 2026  
**Context:** TryHackMe training environment; simulated management decisions

## Decision requested
Approve the proposed remediation sequence and nominate accountable owners. Validate the potential remote file inclusion (RFI) flag within two days, address anonymous FTP access within seven days, and schedule application hardening over the following two weeks. These are proposed deadlines, not approved commitments.

## Assessment and business impact
The assessment combines the user's Nikto excerpt, a lab-progress screenshot, and TryHackMe's published OpenVAS report images. Nine items are tracked across these sources; this is not a claim of nine independently confirmed vulnerabilities or a comprehensive enterprise audit. For prioritization, the scenario assumes an internal application that may handle sensitive files. Actual data sensitivity, exposure, business criticality and compensating controls remain unknown.

**First priority: validate potential RFI and remove unnecessary anonymous access.** Nikto flagged the `file` parameter on `/info.php`; it did not prove remote code execution. Application Engineering should investigate safely and restrict inclusion to approved local resources. OpenVAS reports anonymous FTP login at severity 6.4 (CVE-1999-0497). Infrastructure Operations should verify accessible content and disable anonymous access unless explicitly justified. Neither data theft nor FTP write access has been demonstrated.

**Second priority: reduce information exposure and session risk.** Remove the public phpinfo page (reported severity 5.3), restrict Apache server-status, disable directory indexing, and set HttpOnly on session cookies. These conditions can assist reconnaissance or worsen another attack, but their presence alone does not establish a breach. Proposed owners are Application Engineering and Web Operations; target completion is October 17.

**Third priority: validate and harden lower-priority conditions.** Review framing protections before treating a missing X-Frame-Options header as exploitable; an appropriate CSP may provide equivalent protection. Validate the DEBUG method flag, and restrict ICMP timestamp responses where appropriate (reported severity 2.1, CVE-1999-0524). Target completion is November 2.

## Governance and accountability
The proposed technical owners implement changes; a designated business risk owner approves priorities, exceptions and residual-risk decisions. Review the POA&M weekly and distinguish validation, implementation and evidence-based closure. Any risk acceptance must name an approver, compensating controls, rationale and expiration or review date. Scanner severity informs triage but does not by itself establish business risk or regulatory noncompliance.

## Assurance and follow-up
All remediation remains proposed or pending validation. Close an item only after configuration evidence, an authorized retest and a functionality check demonstrate the intended result. Residual risk is unvalidated; scanner severity is not a complete business-risk calculation. Review progress weekly, escalate missed proposed dates after owners approve them, and document any accepted risk with an approver, rationale and review date.

**Evidence:** See the accompanying POA&M and [evidence register](evidence/README.md). This project demonstrates assessment and remediation planning; it does not claim production experience, implemented fixes or regulatory compliance.

## Supplemental scan activity
The assessor also ran `nmap -A 127.0.0.1` (Nmap aggressive mode) within the TryHackMe AttackBox. The screenshot captures partial localhost service-discovery output. This separate exercise does not expand the nine assessed Nikto/OpenVAS items or demonstrate fixes. Room completion is documented in the accompanying screenshot. See the evidence register for both images.

