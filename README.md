# THM Vuln Nikto Scan

## Vulnerability Risk & Remediation Assessment

A GRC portfolio project based on the TryHackMe Vulnerability Scanning Tools room, completed October 3, 2026.

## Deliverables
- `FINDINGS.md`: GRC findings summary, priority rationale and risk governance.
- `Project_1_Vulnerability_Risk_POAM.xlsx`: prioritized findings, proposed owners and deadlines, closure requirements, and evidence register.
- `Project_1_Executive_Risk_Memo.md`: management recommendation.
- `evidence/`: user screenshot, supplied scan excerpt and explicitly labeled platform reference images.

## Scope and integrity
This is a simulated assessment and remediation-management exercise. The user completed the room; a completion screenshot is included, but no full scan export was supplied. Business assumptions, proposed owners and deadlines are fictional. No remediation or exploit validation is claimed. Nine items combine Nikto and published OpenVAS observations; they are not nine proven exploits. The potential RFI flag requires validation.

## Skills demonstrated
Evidence review, vulnerability triage, business-impact reasoning, remediation planning, accountability design, closure criteria and executive communication.

## Next actions
Add any original exports you retained. If permitted by the platform, perform authorized validation and document configuration changes and retests. Keep this repository's statuses aligned with actual work completed.

## Supplemental Nmap scan

I also ran an Nmap aggressive scan using `nmap -A 127.0.0.1` in the TryHackMe AttackBox on October 3, 2026. The supplied screenshot shows localhost service discovery, including OpenSSH, dnsmasq and rpcbind. This is a scan of the AttackBox itself, separate from the Nikto/OpenVAS target evidence; it does not establish additional target vulnerabilities or completed remediation. Only partial output is captured.

Evidence: [Nmap aggressive localhost scan](evidence/nmap-aggressive-localhost.png) and [room completion](evidence/thm-room-completion.png).

