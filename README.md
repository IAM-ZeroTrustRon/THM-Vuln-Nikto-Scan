# THM Vuln Nikto Scan

**Ron Richardson | GRC portfolio | October 3, 2026**

I completed TryHackMe's Vulnerability Scanning Tools room and translated its scan observations into a business-risk assessment and a proposed remediation plan. The project demonstrates how I separate scanner output from validated risk and communicate the decisions management needs to make.

## Read the project

| Document | Purpose |
|---|---|
| [Executive risk memo](Project_1_Executive_Risk_Memo.md) | Management recommendation and decisions requested |
| [Findings analysis](FINDINGS.md) | Evidence, control gaps, business consequences and validation questions for nine observations |
| [POA&M workbook](Project_1_Vulnerability_Risk_POAM.xlsx) | Proposed owners, target dates, status and closure requirements |
| [Evidence register](evidence/README.md) | Source files, screenshots and provenance limitations |

## Scope

This is a training exercise with a fictional business context. Nikto and published OpenVAS material underpin the assessment; no implemented fixes or successful exploitation are claimed. The nine tracked observations are not nine proven exploits.

I also ran `nmap -A 127.0.0.1` in the AttackBox. That aggressive-mode localhost scan is a separate learning activity, documented in the evidence register.

[View room completion](evidence/thm-room-completion.png).
