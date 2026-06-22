# Splunk Workbook Section Index

[README](../README.md) | [Proof Map](../reviewer-proof-map.md)

This folder contains the five reviewer-facing section guides for the SOC Analyst Splunk Operations Workbook.

## Recommended Review Order

| Priority | Section | Why review it |
|---|---|---|
| 1 | [Section 04 - Data Parsing, Normalization, and Field Extraction](04-data-parsing-normalization-and-field-extraction.md) | Strongest Splunk configuration proof: event breaking, multiline parsing, masking, transforms, indexed fields, and validation. |
| 2 | [Section 05 - Applied Parsing Fix and Network Log Analysis](05-applied-parsing-fix-and-network-log-analysis.md) | Shows broken-log repair, field extraction, validation, and network analysis. |
| 3 | [Section 01 - SPL Fundamentals and Detection Queries](01-spl-fundamentals-and-detection-queries.md) | Shows SPL triage, filtering, enrichment, and anomaly logic. |
| 4 | [Section 02 - Splunk Lab Deployment and Log Ingestion](02-splunk-lab-deployment-and-log-ingestion.md) | Shows Splunk service validation, forwarder setup, index creation, and log ingestion checks. |
| 5 | [Section 03 - Reports, Alerts, and Dashboards](03-reports-alerts-and-dashboards.md) | Shows reusable reports, dashboard panels, and alert-candidate SPL. |

## Section Guides

| Section | Guide | Related SPL | Evidence |
|---|---|---|---|
| 01 | [SPL Fundamentals and Detection Queries](01-spl-fundamentals-and-detection-queries.md) | [01-spl-fundamentals.spl](../spl/01-spl-fundamentals.spl) | [Screenshots 01-17](../screenshots/01-splunk-exploring-spl/) |
| 02 | [Splunk Lab Deployment and Log Ingestion](02-splunk-lab-deployment-and-log-ingestion.md) | [02-ingestion-validation.spl](../spl/02-ingestion-validation.spl) | [Screenshots 18-33](../screenshots/02-splunk-setting-up-soc-lab/) |
| 03 | [Reports, Alerts, and Dashboards](03-reports-alerts-and-dashboards.md) | [03-reports-alerts-dashboards.spl](../spl/03-reports-alerts-dashboards.spl) | [Screenshots 34-42](../screenshots/03-splunk-dashboards-and-reports/) |
| 04 | [Data Parsing, Normalization, and Field Extraction](04-data-parsing-normalization-and-field-extraction.md) | [04-data-manipulation-validation.spl](../spl/04-data-manipulation-validation.spl) | [Screenshots 43-67](../screenshots/04-splunk-data-manipulation/) |
| 05 | [Applied Parsing Fix and Network Log Analysis](05-applied-parsing-fix-and-network-log-analysis.md) | [05-fixit-analysis.spl](../spl/05-fixit-analysis.spl) | [Screenshots 68-75](../screenshots/05-splunk-fixit-challenge/) |
