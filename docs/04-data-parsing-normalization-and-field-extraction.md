# Section 04 - Splunk Data Parsing, Normalization, and Field Extraction

[Previous](./03-reports-alerts-and-dashboards.md) | [README](../README.md) | [Proof Map](../reviewer-proof-map.md) | [Docs Index](README.md) | [Next](./05-applied-parsing-fix-and-network-log-analysis.md)

## Purpose

This section documents Splunk data manipulation work that turns poorly structured scripted-input data into searchable, analyst-ready events.

The focus is configuration-driven parsing: scripted inputs, event boundary control, multiline event handling, SEDCMD masking, custom field extraction, indexed fields, and validation searches.

## Analyst Workflow

This section follows a practical log onboarding and parsing workflow:

1. Create an app-scoped Splunk configuration structure.
2. Configure scripted inputs for multiple data sources.
3. Validate that raw events are arriving.
4. Identify broken event boundaries.
5. Repair event breaking with `props.conf`.
6. Handle multiline authentication events.
7. Mask sensitive credit-card-like values before review.
8. Extract custom fields with `transforms.conf`.
9. Register indexed fields with `fields.conf`.
10. Validate that extracted fields support analyst searches and aggregation.

## Skills Demonstrated

| Skill | SOC value |
|---|---|
| App-scoped configuration | Keeps ingestion and parsing logic organized and portable. |
| Scripted inputs | Brings custom log sources into Splunk for analysis. |
| Event boundary repair | Prevents multiple log entries from collapsing into unusable events. |
| Multiline parsing | Preserves related authentication data inside one readable event. |
| `SEDCMD` masking | Reduces exposure of sensitive values in indexed event text. |
| `transforms.conf` extraction | Creates structured fields from raw text patterns. |
| `fields.conf` indexed fields | Makes extracted fields usable for faster analyst pivots. |
| Validation searches | Confirms that configuration changes produced usable fields. |

## Configuration Files

| File | Purpose |
|---|---|
| [configs/dataapp/inputs.conf](../configs/dataapp/inputs.conf) | Defines DataApp scripted inputs for sample logs, VPN logs, authentication logs, and purchase logs. |
| [configs/dataapp/props.conf](../configs/dataapp/props.conf) | Defines event-breaking, multiline parsing, masking, and transform references for DataApp sourcetypes. |
| [configs/dataapp/transforms.conf](../configs/dataapp/transforms.conf) | Defines custom field extraction for VPN and purchase events. |
| [configs/dataapp/fields.conf](../configs/dataapp/fields.conf) | Registers extracted fields as indexed fields. |

## Evidence Map

| Screenshot | What it proves |
|---|---|
| [43-splunk-dataapp-created-in-manage-apps.png](../screenshots/04-splunk-data-manipulation/task-05-splunk-app/43-splunk-dataapp-created-in-manage-apps.png) | Created the DataApp application in Splunk. |
| [44-splunk-dataapp-directory-structure.png](../screenshots/04-splunk-data-manipulation/task-05-splunk-app/44-splunk-dataapp-directory-structure.png) | Confirmed the app directory structure for app-scoped configuration. |
| [45-splunk-dataapp-inputs-conf-scripted-input.png](../screenshots/04-splunk-data-manipulation/task-05-splunk-app/45-splunk-dataapp-inputs-conf-scripted-input.png) | Configured a scripted input in `inputs.conf`. |
| [46-splunk-dataapp-scripted-input-ingestion-validation.png](../screenshots/04-splunk-data-manipulation/task-05-splunk-app/46-splunk-dataapp-scripted-input-ingestion-validation.png) | Validated scripted-input ingestion in Splunk search. |
| [47-splunk-vpnlogs-scripted-input-config.png](../screenshots/04-splunk-data-manipulation/task-06-event-boundaries/47-splunk-vpnlogs-scripted-input-config.png) | Added VPN log scripted input configuration. |
| [48-splunk-vpnlogs-broken-event-boundaries-before-fix.png](../screenshots/04-splunk-data-manipulation/task-06-event-boundaries/48-splunk-vpnlogs-broken-event-boundaries-before-fix.png) | Captured broken VPN event boundaries before repair. |
| [49-splunk-vpnlogs-props-conf-event-boundary-rule.png](../screenshots/04-splunk-data-manipulation/task-06-event-boundaries/49-splunk-vpnlogs-props-conf-event-boundary-rule.png) | Added VPN event boundary rules in `props.conf`. |
| [50-splunk-vpnlogs-fixed-event-boundary-validation.png](../screenshots/04-splunk-data-manipulation/task-06-event-boundaries/50-splunk-vpnlogs-fixed-event-boundary-validation.png) | Validated corrected VPN event boundaries. |
| [51-splunk-authlogs-scripted-input-config.png](../screenshots/04-splunk-data-manipulation/task-07-multiline-events/51-splunk-authlogs-scripted-input-config.png) | Added authentication log scripted input configuration. |
| [52-splunk-authlogs-broken-multiline-before-fix.png](../screenshots/04-splunk-data-manipulation/task-07-multiline-events/52-splunk-authlogs-broken-multiline-before-fix.png) | Captured broken multiline authentication events before repair. |
| [53-splunk-authlogs-props-conf-multiline-rule.png](../screenshots/04-splunk-data-manipulation/task-07-multiline-events/53-splunk-authlogs-props-conf-multiline-rule.png) | Added multiline handling rules in `props.conf`. |
| [54-splunk-authlogs-fixed-multiline-validation.png](../screenshots/04-splunk-data-manipulation/task-07-multiline-events/54-splunk-authlogs-fixed-multiline-validation.png) | Validated corrected multiline authentication events. |
| [55-splunk-purchaselogs-scripted-input-config.png](../screenshots/04-splunk-data-manipulation/task-08-masking-sensitive-data/55-splunk-purchaselogs-scripted-input-config.png) | Added purchase log scripted input configuration. |
| [56-splunk-purchaselogs-props-conf-boundary-rule.png](../screenshots/04-splunk-data-manipulation/task-08-masking-sensitive-data/56-splunk-purchaselogs-props-conf-boundary-rule.png) | Added purchase event boundary handling in `props.conf`. |
| [57-splunk-purchaselogs-props-conf-sedcmd-masking-rule.png](../screenshots/04-splunk-data-manipulation/task-08-masking-sensitive-data/57-splunk-purchaselogs-props-conf-sedcmd-masking-rule.png) | Added `SEDCMD` masking for credit-card-like values. |
| [58-splunk-purchaselogs-masked-validation.png](../screenshots/04-splunk-data-manipulation/task-08-masking-sensitive-data/58-splunk-purchaselogs-masked-validation.png) | Validated that sensitive values were masked in searchable events. |
| [59-splunk-vpn-custom-fields-transforms-conf.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/59-splunk-vpn-custom-fields-transforms-conf.png) | Defined VPN field extraction in `transforms.conf`. |
| [60-splunk-vpn-props-conf-transforms-reference.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/60-splunk-vpn-props-conf-transforms-reference.png) | Referenced VPN transforms from `props.conf`. |
| [61-splunk-vpn-custom-fields-fields-conf.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/61-splunk-vpn-custom-fields-fields-conf.png) | Registered VPN extracted fields in `fields.conf`. |
| [62-splunk-vpn-custom-field-extraction-validation.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/62-splunk-vpn-custom-field-extraction-validation.png) | Validated VPN custom fields in Splunk search. |
| [63-splunk-purchase-custom-fields-transforms-conf.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/63-splunk-purchase-custom-fields-transforms-conf.png) | Defined purchase field extraction in `transforms.conf`. |
| [64-splunk-purchase-props-conf-transforms-reference.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/64-splunk-purchase-props-conf-transforms-reference.png) | Referenced purchase transforms from `props.conf`. |
| [65-splunk-purchase-fields-conf-cc-number.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/65-splunk-purchase-fields-conf-cc-number.png) | Registered purchase extracted fields in `fields.conf`. |
| [66-splunk-purchase-custom-field-extraction-validation.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/66-splunk-purchase-custom-field-extraction-validation.png) | Validated purchase custom fields in Splunk search. |
| [67-splunk-purchase-field-extraction-summary-counts.png](../screenshots/04-splunk-data-manipulation/task-09-custom-field-extraction/67-splunk-purchase-field-extraction-summary-counts.png) | Confirmed extracted purchase fields support aggregation and distinct counts. |

## Parsing Lessons

Raw logs are often not immediately usable. The same data can be present but operationally weak if events are split incorrectly, multiple entries collapse into one event, or important values remain trapped inside `_raw`.

This section demonstrates the progression from raw ingestion to analyst-ready fields:

- `inputs.conf` brings the data in.
- `props.conf` controls event structure and masking.
- `transforms.conf` extracts meaningful fields.
- `fields.conf` registers indexed fields.
- SPL validation confirms that the configuration works.

## Public Safety Note

The purchase log workflow masks credit-card-like values before publishing evidence. The artifact shows the masking and extraction workflow without exposing full sensitive payment data.

## Related SPL

See:

[04-data-manipulation-validation.spl](../spl/04-data-manipulation-validation.spl)
