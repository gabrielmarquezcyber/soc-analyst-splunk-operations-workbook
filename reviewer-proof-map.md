# Reviewer Proof Map

This page is the fastest way to review the SOC Analyst Splunk Operations Workbook.

It maps each section to the exact proof a reviewer should inspect: section guide, SPL file, configuration files, and screenshot evidence.

## Visual First Review

Start with the screenshot-driven visual page if you want the fastest human-readable view of the artifact:

- [Visual Walkthrough](docs/visual-walkthrough.md)

## Fastest Review Order

| Priority | What to review | Why it matters |
|---|---|---|
| 1 | [Visual Walkthrough](docs/visual-walkthrough.md) | Screenshot-driven narrative showing the workbook as a reviewer-friendly investigation story. |
| 2 | [Section 04 - Data Parsing, Normalization, and Field Extraction](docs/04-data-parsing-normalization-and-field-extraction.md) | Strongest proof of Splunk configuration depth: event breaking, multiline parsing, masking, transforms, fields, and validation. |
| 3 | [Section 05 - Applied Parsing Fix and Network Log Analysis](docs/05-applied-parsing-fix-and-network-log-analysis.md) | Shows broken-log diagnosis, parsing repair, custom field extraction, and structured network analysis. |
| 4 | [Section 01 - SPL Fundamentals and Detection Queries](docs/01-spl-fundamentals-and-detection-queries.md) | Shows SPL triage progression from basic searches to enrichment and anomaly logic. |
| 5 | [Section 02 - Splunk Lab Deployment and Log Ingestion](docs/02-splunk-lab-deployment-and-log-ingestion.md) | Shows Splunk service validation, forwarder flow, index creation, and ingestion checks. |
| 6 | [Section 03 - Reports, Alerts, and Dashboards](docs/03-reports-alerts-and-dashboards.md) | Shows reusable reports, dashboard panels, and alert-candidate SPL. |

## Proof Summary

| Area | Guide | Technical files | Screenshot evidence |
|---|---|---|---|
| SPL triage and anomaly logic | [Section 01](docs/01-spl-fundamentals-and-detection-queries.md) | [01-spl-fundamentals.spl](spl/01-spl-fundamentals.spl) | [Screenshots 01-17](screenshots/01-splunk-exploring-spl/) |
| Splunk deployment and ingestion | [Section 02](docs/02-splunk-lab-deployment-and-log-ingestion.md) | [02-ingestion-validation.spl](spl/02-ingestion-validation.spl) | [Screenshots 18-33](screenshots/02-splunk-setting-up-soc-lab/) |
| Reports, alerts, dashboards | [Section 03](docs/03-reports-alerts-and-dashboards.md) | [03-reports-alerts-dashboards.spl](spl/03-reports-alerts-dashboards.spl) | [Screenshots 34-42](screenshots/03-splunk-dashboards-and-reports/) |
| Parsing, masking, field extraction | [Section 04](docs/04-data-parsing-normalization-and-field-extraction.md) | [DataApp configs](configs/dataapp/), [04 SPL validation](spl/04-data-manipulation-validation.spl) | [Screenshots 43-67](screenshots/04-splunk-data-manipulation/) |
| Applied network-log repair | [Section 05](docs/05-applied-parsing-fix-and-network-log-analysis.md) | [Fixit configs](configs/fixit/), [05 SPL analysis](spl/05-fixit-analysis.spl) | [Screenshots 68-75](screenshots/05-splunk-fixit-challenge/) |

## What To Look For

### 1. SPL Triage

The workbook starts with basic but important analyst behaviors:

- Validate searchable data.
- Count events.
- Identify high-volume values.
- Narrow by time.
- Filter by EventID, host, IP, and port.
- Structure output with tables.
- Use enrichment and lookup context.
- Apply baseline logic for unusual VPN activity.

Primary proof:

- [Section 01 guide](docs/01-spl-fundamentals-and-detection-queries.md)
- [01 SPL searches](spl/01-spl-fundamentals.spl)
- [Section 01 screenshots](screenshots/01-splunk-exploring-spl/)

### 2. Ingestion and Metadata Validation

This section proves the user understands that Splunk analysis depends on trustworthy data ingestion and metadata.

Primary proof:

- Splunk Enterprise path validation
- Splunk Web availability
- CLI service status
- Universal Forwarder validation
- TCP receiving on port `9997`
- Linux auth index creation
- Auth log ingestion validation
- Apache access log ingestion validation

Primary proof:

- [Section 02 guide](docs/02-splunk-lab-deployment-and-log-ingestion.md)
- [02 SPL searches](spl/02-ingestion-validation.spl)
- [Section 02 screenshots](screenshots/02-splunk-setting-up-soc-lab/)

### 3. Reports, Alert-Candidate Logic, and Dashboards

This section shows how recurring analyst questions become reusable Splunk assets.

Primary proof:

- VPN login report
- Web connections by source IP
- Restricted-page external source IP logic
- Payment-page 404 count
- Hourly 404 threshold logic
- Dashboard panels for URI, status code, and source activity

Primary proof:

- [Section 03 guide](docs/03-reports-alerts-and-dashboards.md)
- [03 SPL searches](spl/03-reports-alerts-dashboards.spl)
- [Section 03 screenshots](screenshots/03-splunk-dashboards-and-reports/)

### 4. Parsing, Masking, and Field Extraction

This is the strongest Splunk operations section. It shows app-scoped configuration and parsing mechanics, not just searches.

Primary proof:

- Scripted inputs
- Event boundary repair
- Multiline authentication event handling
- SEDCMD masking
- Regex field extraction
- Indexed field registration
- Validation searches proving extracted fields are usable

Primary proof:

- [Section 04 guide](docs/04-data-parsing-normalization-and-field-extraction.md)
- [DataApp inputs.conf](configs/dataapp/inputs.conf)
- [DataApp props.conf](configs/dataapp/props.conf)
- [DataApp transforms.conf](configs/dataapp/transforms.conf)
- [DataApp fields.conf](configs/dataapp/fields.conf)
- [04 SPL validation](spl/04-data-manipulation-validation.spl)
- [Section 04 screenshots](screenshots/04-splunk-data-manipulation/)

### 5. Applied Network-Log Repair

This section proves the end-to-end workflow: broken logs, parsing repair, field extraction, validation, and final analysis.

Primary proof:

- Broken event review
- Scripted-input confirmation
- Event boundary repair using `BREAK_ONLY_BEFORE`
- Extraction of `Username`, `Department`, `Domain`, `URI`, `SourceIP`, and `Country`
- Indexed field registration
- Network activity summary analysis

Primary proof:

- [Section 05 guide](docs/05-applied-parsing-fix-and-network-log-analysis.md)
- [Fixit inputs.conf](configs/fixit/inputs.conf)
- [Fixit props.conf](configs/fixit/props.conf)
- [Fixit transforms.conf](configs/fixit/transforms.conf)
- [Fixit fields.conf](configs/fixit/fields.conf)
- [05 SPL analysis](spl/05-fixit-analysis.spl)
- [Section 05 screenshots](screenshots/05-splunk-fixit-challenge/)

## Validated Network Analysis Results

| Question | Result |
|---|---|
| Primary domain observed | `Cybertees.THM` |
| Unique username values | `28` |
| Unique URI values | `12` |
| Individual `/products/` pages | `2` |
| URI without a file extension | `/sales/` |
| Most active user | `Robert Wilson` |
| Unique private IP range families | `3` |
| User associated with `/secret-document.pdf` | `Sarah Hall` |

## Scope

This artifact demonstrates Splunk analyst workflow, log onboarding awareness, parsing configuration, field extraction, validation searches, dashboard/report construction, and evidence documentation.

It does not claim production ownership of an enterprise Splunk deployment.

## Return to README

[Back to main README](README.md)
