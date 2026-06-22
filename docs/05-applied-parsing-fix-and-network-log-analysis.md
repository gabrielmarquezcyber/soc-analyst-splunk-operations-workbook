# Section 05 - Applied Splunk Parsing Fix and Network Log Analysis

[Previous](./04-data-parsing-normalization-and-field-extraction.md) | [README](../README.md) | [Proof Map](../reviewer-proof-map.md) | [Docs Index](README.md) | Next

## Purpose

This section documents an applied parsing repair workflow for broken network-log data. The goal is to show how an analyst can diagnose unusable events, repair parsing with Splunk configuration, extract custom fields, validate the result, and then answer investigation questions from structured data.

This section ties together the previous workbook skills:

1. Inspect broken events.
2. Identify the correct app and scripted-input path.
3. Repair event boundaries.
4. Extract fields from raw network-log text.
5. Register indexed fields.
6. Validate field extraction in Splunk search.
7. Use SPL to produce an analyst-ready network activity summary.

## Analyst Workflow

The workflow follows a realistic parsing and investigation path:

1. Review the broken network events.
2. Confirm the Splunk app path.
3. Confirm the scripted-input path.
4. Update `inputs.conf` for the network log source.
5. Repair event boundaries in `props.conf`.
6. Define field extraction in `transforms.conf`.
7. Register extracted fields in `fields.conf`.
8. Validate that `Username`, `Department`, `Domain`, `URI`, `SourceIP`, and `Country` are searchable.
9. Run summary analysis against the repaired dataset.

## Skills Demonstrated

| Skill | SOC value |
|---|---|
| Broken event review | Identifies why raw data is not analyst-ready. |
| Scripted-input validation | Confirms where custom logs enter Splunk. |
| Event boundary repair | Prevents unrelated network records from merging together. |
| Regex-based field extraction | Turns raw text into structured investigation fields. |
| Indexed field registration | Supports faster pivots on important extracted values. |
| Field validation search | Confirms that parsing changes worked before analysis. |
| Network activity aggregation | Produces summary values from repaired data. |
| Private IP range grouping | Supports source IP family analysis. |
| Sensitive document access review | Identifies user activity tied to a sensitive-looking URI. |

## Configuration Files

| File | Purpose |
|---|---|
| [configs/fixit/inputs.conf](../configs/fixit/inputs.conf) | Defines the scripted input for the network log source. |
| [configs/fixit/props.conf](../configs/fixit/props.conf) | Defines event boundary handling and transform reference for `network_logs`. |
| [configs/fixit/transforms.conf](../configs/fixit/transforms.conf) | Extracts `Username`, `Department`, `Domain`, `URI`, `SourceIP`, and `Country`. |
| [configs/fixit/fields.conf](../configs/fixit/fields.conf) | Registers extracted network fields as indexed fields. |

## Evidence Map

| Screenshot | What it proves |
|---|---|
| [68-splunk-fixit-initial-broken-events.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/68-splunk-fixit-initial-broken-events.png) | Captured the initial broken network events before parsing repair. |
| [69-splunk-fixit-app-inputs-conf-network-logs.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/69-splunk-fixit-app-inputs-conf-network-logs.png) | Confirmed the network log scripted-input configuration. |
| [70-splunk-fixit-props-conf-event-boundary-fix.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/70-splunk-fixit-props-conf-event-boundary-fix.png) | Added event boundary repair using `BREAK_ONLY_BEFORE`. |
| [71-splunk-fixit-transforms-conf-custom-fields.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/71-splunk-fixit-transforms-conf-custom-fields.png) | Defined custom field extraction for network log values. |
| [72-splunk-fixit-props-conf-transforms-reference.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/72-splunk-fixit-props-conf-transforms-reference.png) | Referenced the field extraction transform from `props.conf`. |
| [73-splunk-fixit-fields-conf-indexed-fields.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/73-splunk-fixit-fields-conf-indexed-fields.png) | Registered extracted network fields in `fields.conf`. |
| [74-splunk-fixit-fixed-field-extraction-validation.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/74-splunk-fixit-fixed-field-extraction-validation.png) | Validated that extracted fields appeared in Splunk search results. |
| [75-splunk-fixit-network-analysis-summary.png](../screenshots/05-splunk-fixit-challenge/task-02-fixit-challenge/75-splunk-fixit-network-analysis-summary.png) | Produced the final structured network analysis summary. |

## Key Technical Details

| Item | Value |
|---|---|
| App path | `/opt/splunk/etc/apps/fixit` |
| Script path | `/opt/splunk/etc/apps/fixit/bin/network-logs` |
| Source | `networks` |
| Sourcetype | `network_logs` |
| Event boundary setting | `BREAK_ONLY_BEFORE` |
| Event boundary regex | `\[Network-log\]:` |
| Extracted fields | `Username`, `Department`, `Domain`, `URI`, `SourceIP`, `Country` |

## Validated Analysis Results

| Investigation question | Validated result |
|---|---|
| Primary domain observed | `Cybertees.THM` |
| Unique username values | `28` |
| Unique URI values | `12` |
| Individual `/products/` pages | `2` |
| URI without a file extension | `/sales/` |
| Most active user | `Robert Wilson` |
| Unique private IP range families | `3` |
| User associated with `/secret-document.pdf` | `Sarah Hall` |

## Parsing Lessons

The important lesson is that the data was not missing. It was poorly structured.

Before the repair, the logs were difficult to analyze because event boundaries and fields were not usable. After the repair, the same raw data could support direct questions about domains, users, URIs, IP ranges, and sensitive-looking document access.

The practical sequence is:

- Fix event boundaries first.
- Extract fields second.
- Register fields third.
- Validate fields fourth.
- Analyze only after the data is trustworthy.

## Analyst Notes

This section is a useful SOC proof point because it shows the difference between searching raw logs and operationalizing raw logs.

A strong analyst does not only write searches. They also validate whether the data model, sourcetype, event boundaries, and field extractions are usable. Bad parsing creates bad analysis, even when the original log source contains the right evidence.

## Public Safety Note

The published evidence avoids credentials and private secrets. Sensitive-looking paths are treated as investigation artifacts, not as content to expose.

## Related SPL

See:

[05-fixit-analysis.spl](../spl/05-fixit-analysis.spl)
