# Section 01 - SPL Fundamentals and Detection Queries

## Purpose

This section documents foundational SPL workflows for SOC triage. It starts with basic dataset validation, then moves into field filtering, time-bounded searches, EventID pivots, network field filtering, table output, regex matching, enrichment, lookup context, and anomaly detection.

The progression mirrors a practical analyst workflow:

1. Confirm the dataset is searchable.
2. Identify high-volume values.
3. Narrow by time window.
4. Filter by event type.
5. Pivot on host, source, destination, and port.
6. Structure results for readable review.
7. Add context through enrichment and lookups.
8. Apply baseline logic for unusual VPN activity.

## Skills Demonstrated

| SPL concept | SOC use |
|---|---|
| `stats count` | Validate dataset size and event availability. |
| `stats count by <field>` | Identify high-frequency values for investigation pivots. |
| `sort - count` | Rank high-volume values. |
| `head` | Limit review to top results. |
| `earliest` / `latest` | Narrow analysis to a specific investigation window. |
| `field=value` filters | Isolate events by attributes such as EventID, host, IP, or port. |
| wildcard keyword search | Test broad term matching across indexed data. |
| `fields` | Reduce visible data to investigation-relevant fields. |
| `table` | Produce analyst-readable output. |
| `reverse` | Review event order from oldest to newest. |
| `regex` | Match field patterns such as registry paths or object names. |
| `top` | Summarize frequent values quickly. |
| `iplocation` | Add geographic context to source IPs. |
| `lookup` | Add external risk or context values. |
| `eventstats` | Calculate behavioral context while preserving event-level detail. |
| `eval` | Create derived values such as login hour or z-score. |
| `where` | Filter events based on calculated conditions. |

## Evidence Map

| Screenshot | What it proves |
|---|---|
| [01-splunk-windowslogs-base-event-count.png](../screenshots/01-splunk-exploring-spl/task-02-search-reporting/01-splunk-windowslogs-base-event-count.png) | Validated basic event counting against the Windows log dataset. |
| [02-splunk-top-sourceip-frequency-analysis.png](../screenshots/01-splunk-exploring-spl/task-02-search-reporting/02-splunk-top-sourceip-frequency-analysis.png) | Identified high-frequency SourceIp values in Windows event data. |
| [03-splunk-time-bounded-event-count.png](../screenshots/01-splunk-exploring-spl/task-02-search-reporting/03-splunk-time-bounded-event-count.png) | Counted events inside a narrow investigation window. |
| [04-splunk-eventid-4624-equality-filter.png](../screenshots/01-splunk-exploring-spl/task-03-search-operators/04-splunk-eventid-4624-equality-filter.png) | Filtered Windows logs by EventID 4624 and counted matching successful-logon events. |
| [05-splunk-destinationip-port-compound-filter.png](../screenshots/01-splunk-exploring-spl/task-03-search-operators/05-splunk-destinationip-port-compound-filter.png) | Filtered by destination IP and destination port to scope network activity. |
| [06-splunk-host-destination-sourceip-analysis.png](../screenshots/01-splunk-exploring-spl/task-03-search-operators/06-splunk-host-destination-sourceip-analysis.png) | Combined hostname, destination IP, and SourceIp presence, then aggregated by SourceIp. |
| [07-splunk-wildcard-keyword-search-cyber.png](../screenshots/01-splunk-exploring-spl/task-03-search-operators/07-splunk-wildcard-keyword-search-cyber.png) | Used wildcard keyword search to validate broad term matching. |
| [08-splunk-fields-sourceprocessid-filtering.png](../screenshots/01-splunk-exploring-spl/task-04-filtering-results/08-splunk-fields-sourceprocessid-filtering.png) | Used `fields` to narrow visible data and exposed a process ID data-quality issue. |
| [09-splunk-regex-targetobject-manager.png](../screenshots/01-splunk-exploring-spl/task-04-filtering-results/09-splunk-regex-targetobject-manager.png) | Used regex filtering to identify TargetObject values ending in Manager. |
| [10-splunk-table-account-fields.png](../screenshots/01-splunk-exploring-spl/task-05-structuring-results/10-splunk-table-account-fields.png) | Structured account-related fields into a readable analyst table. |
| [11-splunk-reverse-account-event-table.png](../screenshots/01-splunk-exploring-spl/task-05-structuring-results/11-splunk-reverse-account-event-table.png) | Used `reverse` to inspect account activity from oldest to newest. |
| [12-splunk-process-timeline-a1berto-password-redacted.png](../screenshots/01-splunk-exploring-spl/task-05-structuring-results/12-splunk-process-timeline-a1berto-password-redacted.png) | Reconstructed a process timeline while redacting credential-like material. |
| [13-splunk-top-image-frequency-analysis.png](../screenshots/01-splunk-exploring-spl/task-06-transforming-commands/13-splunk-top-image-frequency-analysis.png) | Used `top` to identify the most frequent process image. |
| [14-splunk-iplocation-sourceip-region-enrichment.png](../screenshots/01-splunk-exploring-spl/task-06-transforming-commands/14-splunk-iplocation-sourceip-region-enrichment.png) | Used `iplocation` to enrich SourceIp values with geographic context. |
| [15-splunk-lookup-image-riskscore-enrichment.png](../screenshots/01-splunk-exploring-spl/task-06-transforming-commands/15-splunk-lookup-image-riskscore-enrichment.png) | Used lookup enrichment to add RiskScore context to process images. |
| [16-splunk-vpn-rare-country-outlier-detection.png](../screenshots/01-splunk-exploring-spl/task-07-anomaly-detection/16-splunk-vpn-rare-country-outlier-detection.png) | Used per-user country frequency logic to detect rare VPN login geography. |
| [17-splunk-vpn-login-hour-zscore-outlier.png](../screenshots/01-splunk-exploring-spl/task-07-anomaly-detection/17-splunk-vpn-login-hour-zscore-outlier.png) | Used login-hour z-score logic to identify unusual VPN login timing. |

## Analyst Notes

The early searches establish a foundation: count the data, inspect common values, narrow by time, and filter by important fields. This matters because a SOC analyst should not jump straight into complex detection logic before confirming that the dataset, fields, and investigation window are correct.

The middle portion focuses on making event data readable. `fields`, `table`, `reverse`, and `regex` help turn raw events into structured investigation views. This is the difference between having logs and being able to review them under time pressure.

The final portion introduces enrichment and anomaly logic. `iplocation`, `lookup`, `eventstats`, `eval`, and `where` show how raw events can be enriched, baselined, and filtered into higher-signal results.

## Data Quality Lesson

One field-selection task exposed a practical SPL issue: fields that look numeric may contain mixed formats, such as decimal and hex-like values. Before relying on sort order, analysts should validate field format and type assumptions.

This matters in real triage because incorrect assumptions about field types can change which values appear most important.

## Public Safety Note

The process timeline screenshot was redacted before publication because the original command line contained credential-like material. The public artifact preserves the process relationship and timeline evidence without exposing the sensitive value.

## Related SPL

See:

[01-spl-fundamentals.spl](../spl/01-spl-fundamentals.spl)
