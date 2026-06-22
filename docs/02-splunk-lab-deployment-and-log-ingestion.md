# Section 02 - Splunk Lab Deployment and Log Ingestion

[Previous](./01-spl-fundamentals-and-detection-queries.md) | [README](../README.md) | [Proof Map](../reviewer-proof-map.md) | [Docs Index](README.md) | [Next](./03-reports-alerts-and-dashboards.md)

## Purpose

This section documents the operational foundation behind Splunk analysis: service startup, CLI validation, forwarder concepts, receiving configuration, index creation, monitored file inputs, and ingestion validation.

The goal is to show that Splunk data is not useful until an analyst can confirm that it is arriving with correct source, sourcetype, host, and index metadata.

## Analyst Workflow

This section follows the path from Splunk deployment to searchable logs:

1. Confirm Splunk Enterprise is installed and running.
2. Validate Splunk Web and CLI service status.
3. Confirm Universal Forwarder installation and service status.
4. Configure Splunk to receive forwarded events.
5. Create a dedicated index for Linux authentication logs.
6. Configure monitored file inputs.
7. Validate Linux auth log ingestion.
8. Configure Apache access log ingestion.
9. Validate web log metadata and field usability.

## Skills Demonstrated

| Skill | SOC value |
|---|---|
| Splunk Enterprise startup validation | Confirms the platform is available before analysis. |
| CLI service checks | Supports troubleshooting outside the web interface. |
| Universal Forwarder validation | Confirms endpoint or server log shipping components are active. |
| Receiving port configuration | Enables Splunk to receive forwarded data. |
| Index creation | Separates data by purpose and supports targeted searches. |
| Monitored file input configuration | Onboards log files for security review. |
| Metadata validation | Confirms source, sourcetype, host, and index before relying on data. |
| Web log onboarding | Enables URI, response-code, and web activity analysis. |

## Evidence Map

| Screenshot | What it proves |
|---|---|
| [18-splunk-linux-install-directory-opt.png](../screenshots/02-splunk-setting-up-soc-lab/task-03-linux-deployment/18-splunk-linux-install-directory-opt.png) | Confirmed Splunk Enterprise is installed under `/opt/splunk`. |
| [19-splunk-enterprise-running-web-port-8000.png](../screenshots/02-splunk-setting-up-soc-lab/task-03-linux-deployment/19-splunk-enterprise-running-web-port-8000.png) | Started Splunk Enterprise and confirmed Splunk Web availability on port `8000`. |
| [20-splunk-cli-status-running.png](../screenshots/02-splunk-setting-up-soc-lab/task-04-managing-splunk-cli/20-splunk-cli-status-running.png) | Validated Splunk service status from the CLI. |
| [21-splunk-universal-forwarder-install-directory.png](../screenshots/02-splunk-setting-up-soc-lab/task-05-universal-forwarder/21-splunk-universal-forwarder-install-directory.png) | Confirmed Universal Forwarder installation under `/opt/splunkforwarder`. |
| [22-splunk-universal-forwarder-running.png](../screenshots/02-splunk-setting-up-soc-lab/task-05-universal-forwarder/22-splunk-universal-forwarder-running.png) | Confirmed the Universal Forwarder service was running. |
| [23-splunk-receiving-port-9997-enabled.png](../screenshots/02-splunk-setting-up-soc-lab/task-06-configuring-forwarder/23-splunk-receiving-port-9997-enabled.png) | Enabled Splunk receiving on TCP port `9997`. |
| [24-splunk-linux-host-index-created.png](../screenshots/02-splunk-setting-up-soc-lab/task-06-configuring-forwarder/24-splunk-linux-host-index-created.png) | Created the `linux_host` index for Linux authentication log ingestion. |
| [25-splunk-forwarder-output-to-indexer-9997.png](../screenshots/02-splunk-setting-up-soc-lab/task-06-configuring-forwarder/25-splunk-forwarder-output-to-indexer-9997.png) | Configured the forwarder to send output to `127.0.0.1:9997`. |
| [26-splunk-forwarder-authlog-monitor-inputs.png](../screenshots/02-splunk-setting-up-soc-lab/task-06-configuring-forwarder/26-splunk-forwarder-authlog-monitor-inputs.png) | Configured the forwarder to monitor `/var/log/auth.log` and send it to `linux_host`. |
| [27-splunk-authlog-ingestion-sourcetype-validation.png](../screenshots/02-splunk-setting-up-soc-lab/task-06-configuring-forwarder/27-splunk-authlog-ingestion-sourcetype-validation.png) | Validated Linux authentication log ingestion by sourcetype, source, and host. |
| [28-splunk-adduser-analyst-process-validation.png](../screenshots/02-splunk-setting-up-soc-lab/task-06-configuring-forwarder/28-splunk-adduser-analyst-process-validation.png) | Confirmed user creation activity appeared in Linux auth logs and exposed `process=adduser`. |
| [29-splunk-apache-accesslog-monitor-config.png](../screenshots/02-splunk-setting-up-soc-lab/task-08-ingesting-web-logs/29-splunk-apache-accesslog-monitor-config.png) | Configured Apache access log ingestion into the `web` index. |
| [30-splunk-web-accesslog-ingestion-validation.png](../screenshots/02-splunk-setting-up-soc-lab/task-08-ingesting-web-logs/30-splunk-web-accesslog-ingestion-validation.png) | Validated Apache access log ingestion by index, host, source, and sourcetype. |
| [31-splunk-web-root-field-frequency-analysis.png](../screenshots/02-splunk-setting-up-soc-lab/task-08-ingesting-web-logs/31-splunk-web-root-field-frequency-analysis.png) | Used the `root` field to identify high-count web path categories. |
| [32-splunk-web-cappuchino-uri-path.png](../screenshots/02-splunk-setting-up-soc-lab/task-08-ingesting-web-logs/32-splunk-web-cappuchino-uri-path.png) | Located a specific web resource URI path in Apache access logs. |
| [33-splunk-web-secret-flag-access-validation.png](../screenshots/02-splunk-setting-up-soc-lab/task-08-ingesting-web-logs/33-splunk-web-secret-flag-access-validation.png) | Validated access to a sensitive-looking web path without exposing page content. |

## Key Technical Details

| Item | Value |
|---|---|
| Splunk Enterprise path | `/opt/splunk` |
| Splunk Web port | `8000` |
| Forwarder management port | `8090` in this lab, adjusted because the local Enterprise instance already used `8089` |
| Receiving port | `9997` |
| Linux auth index | `linux_host` |
| Auth log source | `/var/log/auth.log` |
| Auth log sourcetype | `auth` |
| Web index | `web` |
| Apache source | `/var/log/apache2/access.log` |
| Web host | `coffelyweb` |
| Web sourcetype | `access_combined` |

## Analyst Notes

This section matters because SOC analysis depends on data trust. A dashboard, report, or detection search is only as reliable as the data behind it.

Before building detections, an analyst should confirm:

- The expected source is being monitored.
- Events are reaching the correct index.
- The host value is correct.
- The sourcetype matches the log type.
- The field extraction is usable enough for analysis.
- Test events appear when expected.

The Linux authentication workflow validates that account activity can be searched from `/var/log/auth.log`. The Apache workflow validates that web access logs can support URI review, response-code review, and sensitive path investigation.

## Public Safety Note

The sensitive-looking web path validation does not publish page content. It only shows that access to a specific URI can be located in web logs.

## Related SPL

See:

[02-ingestion-validation.spl](../spl/02-ingestion-validation.spl)
