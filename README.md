# SOC Analyst Splunk Operations Workbook

## Executive Summary

This workbook documents a hands-on Splunk SOC operations lab series focused on practical analyst workflows: SPL triage, log ingestion, reports, dashboards, alert-candidate logic, app-scoped configuration, event boundary repair, multiline parsing, SEDCMD masking, custom field extraction, and applied network-log analysis.

The project demonstrates how raw and poorly structured log data can be transformed into searchable, analyst-ready events using Splunk configuration files and validation searches. The final Fixit section applies the same parsing and extraction workflow to repair broken network logs, extract fields, and answer network activity questions from structured Splunk results.

## Portfolio Role

| Field | Details |
|---|---|
| Portfolio Tier | Tier 2 supporting SOC/SIEM operations artifact |
| Primary Value | Splunk operations, SPL triage, log onboarding, parsing, dashboards, and analyst validation |
| Role Alignment | SOC Analyst, MDR Analyst, SIEM Analyst, Security Analyst, Detection Analyst, Security Operations |
| Flagship Relationship | Supports the main portfolio pillars without replacing Elastic SIEM, Azure Cloud Security Governance, or Empire Breacher |

## What This Proves

- Built and validated SPL searches for SOC triage and anomaly detection.
- Configured Splunk Enterprise, receiving ports, indexes, and monitored log sources.
- Validated Linux auth log and Apache access log ingestion by source, sourcetype, host, and index.
- Created reusable reports and dashboard panels for recurring SOC review.
- Built alert-candidate SPL for restricted-page access and HTTP 404 threshold logic.
- Created a custom Splunk app with app-local inputs.conf, props.conf, transforms.conf, and fields.conf.
- Configured scripted inputs for custom log sources.
- Repaired broken event boundaries using SHOULD_LINEMERGE, MUST_BREAK_AFTER, LINE_BREAKER, and BREAK_ONLY_BEFORE.
- Preserved multi-line authentication events as complete records.
- Masked sensitive payment-card-like values with SEDCMD before analysis.
- Extracted custom fields from VPN, purchase, and network logs.
- Used extracted fields for network activity analysis, including user counts, URI counts, product-page activity, sensitive document access, and IP range grouping.

## Reviewer Proof Map

Use the proof map for a guided technical review:

[Reviewer Proof Map](reviewer-proof-map.md)

## Workbook Sections

| Section | Focus | Evidence |
|---|---|---|
| 01 - SPL Fundamentals and Detection Queries | SPL filtering, aggregation, tables, regex, enrichment, lookup context, eventstats, z-score logic | `screenshots/01-splunk-exploring-spl/` |
| 02 - Splunk Lab Deployment and Log Ingestion | Splunk Enterprise startup, Universal Forwarder, receiving port, indexes, Linux auth logs, Apache access logs | `screenshots/02-splunk-setting-up-soc-lab/` |
| 03 - Reports, Alerts, and Dashboards | Reusable reports, alert-candidate SPL, HTTP 404 threshold logic, dashboard panels | `screenshots/03-splunk-dashboards-and-reports/` |
| 04 - Data Parsing, Normalization, and Field Extraction | App-scoped configuration, scripted inputs, event boundaries, multiline events, SEDCMD masking, transforms, fields | `screenshots/04-splunk-data-manipulation/` |
| 05 - Applied Parsing Fix and Network Log Analysis | Broken network-log parsing repair, custom extraction, field validation, final network activity analysis | `screenshots/05-splunk-fixit-challenge/` |

## Public Safety and Scope

This artifact is written as a defender-focused SOC/SIEM workbook.

It does not publish room flags, answer boxes, unmasked payment-card-like values, exposed passwords, or offensive command chains. Sensitive-looking values were redacted or masked where needed. The purpose is to show Splunk analyst workflow, ingestion validation, parsing repair, and field-based analysis discipline.

## Security Operations Value

Splunk work is not only searching. Analysts need to understand whether data is present, whether metadata is correct, whether event boundaries are reliable, whether fields are extracted correctly, and whether dashboards or alert-candidate searches are based on trustworthy data.

This workbook shows the operational path from raw logs to analyst-ready events:

1. Validate dataset availability.
2. Narrow investigation scope with SPL.
3. Structure results for readable review.
4. Enrich and baseline events.
5. Configure ingestion and source metadata.
6. Repair broken parsing.
7. Mask sensitive values.
8. Extract analyst-useful fields.
9. Validate results with repeatable SPL.
10. Use the structured fields for network activity analysis.

## Limitations

- This is a controlled lab artifact, not a production Splunk deployment.
- Alert logic is documented as alert-candidate SPL where license or lab constraints limited full alert configuration.
- Screenshots are used as validation proof, not as a claim of enterprise-scale monitoring coverage.
- The workbook focuses on analyst workflow, parsing, validation, and repeatability.
