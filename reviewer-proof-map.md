# Reviewer Proof Map

This map helps a reviewer quickly understand what each section proves, where the evidence lives, and why it matters for SOC, MDR, and SIEM operations roles.

## Summary

| Section | Skills Proven | Screenshot Evidence | Reviewer Value |
|---|---|---|---|
| 01 - SPL Fundamentals and Detection Queries | SPL filtering, field selection, aggregation, sorting, regex, table output, timeline reconstruction, enrichment, lookup context, eventstats, z-score logic | `screenshots/01-splunk-exploring-spl/` | Shows that raw event data can be queried, narrowed, structured, enriched, and used for anomaly-oriented triage. |
| 02 - Splunk Lab Deployment and Log Ingestion | Splunk Enterprise startup, CLI validation, Universal Forwarder workflow, receiving port setup, index creation, monitored file inputs, ingestion validation | `screenshots/02-splunk-setting-up-soc-lab/` | Shows that the analyst understands how data reaches Splunk and how to validate source, sourcetype, host, and index metadata. |
| 03 - Reports, Alerts, and Dashboards | Saved reports, recurring searches, alert-candidate SPL, web response-code analysis, dashboard panel design | `screenshots/03-splunk-dashboards-and-reports/` | Shows that repeated SOC questions can be converted into reusable searches and dashboard views. |
| 04 - Data Parsing, Normalization, and Field Extraction | App-scoped inputs.conf, props.conf, transforms.conf, fields.conf, scripted inputs, event boundary repair, multiline parsing, SEDCMD masking, custom fields | `screenshots/04-splunk-data-manipulation/` | Shows practical Splunk configuration depth beyond basic searching. |
| 05 - Applied Parsing Fix and Network Log Analysis | Existing app inspection, broken parsing diagnosis, event boundary repair, custom field extraction, indexed fields, final network-log analysis | `screenshots/05-splunk-fixit-challenge/` | Shows an end-to-end repair and analysis workflow using messy logs. |

## Key Evidence by Section

### Section 01 - SPL Fundamentals and Detection Queries

Evidence shows progression from dataset validation to targeted investigation:

- Base event counting.
- Source IP frequency analysis.
- Time-bounded event counting.
- EventID filtering for Windows log review.
- Destination IP and port filtering.
- Host, destination, and source IP pivoting.
- Wildcard keyword matching.
- Field selection and data-quality awareness.
- Regex field filtering.
- Analyst-readable tables.
- Oldest-to-newest timeline review.
- Redacted process timeline reconstruction.
- Process image frequency analysis.
- IP geolocation enrichment.
- Lookup-based risk enrichment.
- Rare VPN country outlier detection.
- Login-hour z-score anomaly detection.

Data-quality note:

The SourceProcessId workflow exposed a practical SPL issue: fields that look numeric may contain mixed formats, such as decimal and hex-like values. Before relying on sort order, analysts should validate field format and type assumptions.

Public-safety note:

The process timeline screenshot was redacted before publication because the original command line contained credential-like material. The public artifact preserves the process relationship and timeline evidence without exposing the sensitive value.

### Section 02 - Splunk Lab Deployment and Log Ingestion

Evidence shows Splunk service validation, forwarder concepts, receiving configuration, index creation, Linux authentication log ingestion, and Apache access log onboarding.

Key technical details:

- Splunk Enterprise path: `/opt/splunk`
- Splunk Web port: `8000`
- Receiving port: `9997`
- Linux auth index: `linux_host`
- Auth log source: `/var/log/auth.log`
- Auth log sourcetype: `auth`
- Web index: `web`
- Apache source: `/var/log/apache2/access.log`
- Web host: `coffelyweb`
- Web sourcetype: `access_combined`

### Section 03 - Reports, Alerts, and Dashboards

Evidence shows reusable SOC searches, saved reports, alert-candidate SPL, HTTP 404 threshold analysis, and dashboard panel hygiene.

Important scope note:

Where full alert creation was limited by lab or license constraints, this workbook uses the wording `alert-candidate SPL` rather than claiming production alert deployment.

### Section 04 - Data Parsing, Normalization, and Field Extraction

Evidence shows the strongest Splunk configuration work in the artifact:

- Custom Splunk app creation.
- App-local scripted inputs.
- VPN event boundary diagnosis and repair.
- Authentication multiline parsing.
- Purchase log event boundary parsing.
- SEDCMD masking of payment-card-like values.
- transforms.conf custom extraction.
- props.conf transform binding.
- fields.conf indexed field definitions.
- SPL validation after each parsing or extraction change.

Sensitive-data note:

Only masked purchase values such as `4111-XXXX-XXXX-XXXX` should appear in public screenshots or docs. Full payment-card-like values must not be published.

### Section 05 - Applied Parsing Fix and Network Log Analysis

Evidence shows a complete applied workflow:

1. Identify broken `network_logs` parsing.
2. Inspect the existing app configuration.
3. Repair event boundaries using `[Network-log]:`.
4. Extract Username, Department, Domain, URI, SourceIP, and Country.
5. Validate field extraction.
6. Use extracted fields for network activity analysis.

Important correction note:

The final screenshot may show `4` for unique IP ranges if the query buckets an `Other` category. The validated private IP range families are:

- `10.x.x.x`
- `172.16.x.x`
- `192.168.x.x`

Final private range count: `3`.

## Review Priority

For a fast technical review, inspect sections in this order:

1. Section 04, because it shows app-scoped Splunk configuration and parsing depth.
2. Section 05, because it applies parsing repair to network analysis.
3. Section 01, because it shows SPL progression from basic triage to anomaly logic.
4. Section 02, because it validates ingestion and forwarding workflow.
5. Section 03, because it shows reusable reports, dashboarding, and alert-candidate SPL.
