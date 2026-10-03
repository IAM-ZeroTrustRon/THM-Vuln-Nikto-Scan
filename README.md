# THM Vuln Nikto Scan

**Ron Richardson | GRC portfolio | October 3, 2026**

This repository packages the results of a TryHackMe vulnerability assessment into a governance-focused deliverable that translates scanner output into business risk, remediation priorities, and evidence tracking.

The project demonstrates how technical findings can be translated into executive communication, operational prioritization, and validated remediation planning.

## Project deliverables

| Artifact | Purpose |
| --- | --- |
| [docs/Executive_Risk_Memo.md](docs/Executive_Risk_Memo.md) | Executive memo summarizing the risk posture and decisions required |
| [docs/FINDINGS.md](docs/FINDINGS.md) | Detailed findings analysis covering evidence, risks, and validation questions |
| [Project_1_Vulnerability_Risk_POAM.xlsx](Project_1_Vulnerability_Risk_POAM.xlsx) | Proposed remediation plan with owners, dates, and closure criteria |
| [evidence/README.md](evidence/README.md) | Evidence register and provenance notes for screenshots and scan artifacts |

## Repository structure

```text
THM-Vuln-Nikto-Scan/
├── README.md
├── docs/
│   ├── README.md
│   ├── Executive_Risk_Memo.md
│   └── FINDINGS.md
├── evidence/
│   ├── README.md
│   ├── nikto-scan-excerpt.txt
│   ├── nmap-aggressive-localhost.png
│   ├── published-openvas-cves.png
│   ├── published-openvas-results.png
│   ├── thm-room-completion.png
│   └── user-lab-progress.png
├── Project_1_Vulnerability_Risk_POAM.xlsx
├── .gitignore
└── .github/   (optional for future automation)
```

## Scope and limitations

This is a training exercise with a fictional business context. The assessment uses Nikto output and published OpenVAS material as supporting evidence, and it does not claim successful exploitation or a fully validated production environment.

The key objective is to show how scanner findings can be framed as:
- business risk
- prioritized remediation actions
- evidence-based governance decisions
- risk communication for non-technical stakeholders

## Executive summary

The project tracks a set of observations including:
- possible remote file inclusion exposure
- anonymous FTP access risk
- exposed diagnostic interfaces such as phpinfo
- weak session cookie protections
- unnecessary directory indexing and status exposure
- missing framing protections and debug method exposure

The recommended posture is validation-first remediation: confirm the most severe items before concluding the application is exploitable, while immediately governing the risks that create information exposure or reconnaissance opportunities.

## Evidence and provenance

All screenshots and scan excerpts are documented in the evidence register to make the project auditable and transparent about what was captured versus what was inferred.

## Final status

This repository is structured as a polished governance and evidence package for a vulnerability assessment engagement and is ready to be used as a portfolio project or submission artifact.
