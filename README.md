# SOC Analyst Splunk Operations Workbook

Splunk SOC operations workbook covering SPL triage, log ingestion, reports, dashboards, alert-candidate logic, parsing, masking, field extraction, indexed fields, and applied network-log analysis.

This repository is a reviewer-facing proof artifact for SOC, MDR, SIEM, detection analyst, and security operations roles. It demonstrates practical Splunk analyst workflows across search, ingestion, dashboarding, parsing configuration, and investigation validation.

## Start Here

| Reviewer path | Link |
|---|---|
| Visual walkthrough | [Visual Walkthrough](docs/visual-walkthrough.md) |
| Proof map | [Reviewer Proof Map](reviewer-proof-map.md) |
| Section guides | [docs/](docs/) |
| SPL searches | [spl/](spl/) |
| Splunk configuration files | [configs/](configs/) |
| Screenshot evidence | [screenshots/](screenshots/) |

## Fast Review Path

For a quick review, follow this order:

1. [Visual Walkthrough](docs/visual-walkthrough.md)
2. [Reviewer Proof Map](reviewer-proof-map.md)
3. [Section 04 - Data Parsing, Normalization, and Field Extraction](docs/04-data-parsing-normalization-and-field-extraction.md)
4. [Section 05 - Applied Parsing Fix and Network Log Analysis](docs/05-applied-parsing-fix-and-network-log-analysis.md)
5. [Section 01 - SPL Fundamentals and Detection Queries](docs/01-spl-fundamentals-and-detection-queries.md)
6. [SPL Validation Searches](spl/)
7. [Splunk Configuration Files](configs/)

## What This Proves

| Capability | Evidence |
|---|---|
| SPL triage and investigation pivots | [Section 01](docs/01-spl-fundamentals-and-detection-queries.md), [01 SPL file](spl/01-spl-fundamentals.spl) |
| Splunk deployment and log ingestion validation | [Section 02](docs/02-splunk-lab-deployment-and-log-ingestion.md), [02 SPL file](spl/02-ingestion-validation.spl) |
| Reports, dashboard panels, and alert-candidate logic | [Section 03](docs/03-reports-alerts-and-dashboards.md), [03 SPL file](spl/03-reports-alerts-dashboards.spl) |
| Event breaking, multiline parsing, masking, and field extraction | [Section 04](docs/04-data-parsing-normalization-and-field-extraction.md), [DataApp configs](configs/dataapp/) |
| Applied broken-log repair and network activity analysis | [Section 05](docs/05-applied-parsing-fix-and-network-log-analysis.md), [Fixit configs](configs/fixit/) |

## Workbook Sections

| Section | Focus | Guide | Evidence |
|---|---|---|---|
| 01 | SPL fundamentals, filtering, enrichment, anomaly logic | [Guide](docs/01-spl-fundamentals-and-detection-queries.md) | [Screenshots 01-17](screenshots/01-splunk-exploring-spl/) |
| 02 | Splunk deployment, forwarder setup, log ingestion | [Guide](docs/02-splunk-lab-deployment-and-log-ingestion.md) | [Screenshots 18-33](screenshots/02-splunk-setting-up-soc-lab/) |
| 03 | Reports, alerts, dashboards, recurring review | [Guide](docs/03-reports-alerts-and-dashboards.md) | [Screenshots 34-42](screenshots/03-splunk-dashboards-and-reports/) |
| 04 | App-scoped parsing, SEDCMD masking, custom fields | [Guide](docs/04-data-parsing-normalization-and-field-extraction.md) | [Screenshots 43-67](screenshots/04-splunk-data-manipulation/) |
| 05 | Broken network-log repair and structured analysis | [Guide](docs/05-applied-parsing-fix-and-network-log-analysis.md) | [Screenshots 68-75](screenshots/05-splunk-fixit-challenge/) |

## Technical Assets

### SPL Searches

| File | Purpose |
|---|---|
| [01-spl-fundamentals.spl](spl/01-spl-fundamentals.spl) | SPL triage, filtering, enrichment, and anomaly searches. |
| [02-ingestion-validation.spl](spl/02-ingestion-validation.spl) | Linux auth log and Apache access log ingestion validation. |
| [03-reports-alerts-dashboards.spl](spl/03-reports-alerts-dashboards.spl) | Report searches, dashboard panels, and alert-candidate logic. |
| [04-data-manipulation-validation.spl](spl/04-data-manipulation-validation.spl) | Parsing, masking, and field extraction validation searches. |
| [05-fixit-analysis.spl](spl/05-fixit-analysis.spl) | Network-log field validation and final analysis summary. |

### Splunk Configuration

| Folder | Purpose |
|---|---|
| [configs/dataapp/](configs/dataapp/) | Scripted inputs, event boundaries, multiline handling, masking, and field extraction for DataApp sourcetypes. |
| [configs/fixit/](configs/fixit/) | Scripted input, event boundary repair, field extraction, and indexed-field registration for network logs. |

## Public Safety and Scope

This is a public portfolio artifact built from authorized lab work. It is designed to demonstrate analyst reasoning, Splunk configuration literacy, validation searches, and evidence documentation.

The artifact does not claim production Splunk administration, enterprise SIEM ownership, or professional incident response authority. It shows practical analyst workflows that map to SOC and MDR work.

Sensitive values are avoided or redacted. The repository focuses on detection logic, parsing mechanics, validation steps, and analyst-ready documentation.

## Portfolio Role

This is a Tier 2 supporting SOC/SIEM operations artifact.

It supports the main portfolio pillars:

1. Elastic SIEM Detection Engineering and Vulnerability Risk Automation
2. Azure Cloud Security Governance
3. Empire Breacher AI Security Research Harness

This workbook adds Splunk-specific proof for roles that mention Splunk, SIEM operations, SOC triage, log ingestion, dashboarding, reporting, parsing, and field extraction.
