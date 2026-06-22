# Section 03 - Reports, Alerts, and Dashboards

## Purpose

This section documents how recurring SOC questions can be converted into reusable Splunk reports, alert-candidate SPL, and dashboard panels.

The focus is not only on creating visuals. The goal is to show how an analyst turns repeatable investigation needs into searches and panels that support faster review.

## Analyst Workflow

This section follows a practical SOC reporting path:

1. Build a recurring VPN login report.
2. Save the report for repeated review.
3. Analyze web connections by source IP.
4. Build alert-candidate SPL for restricted-page access.
5. Count HTTP 404 responses for a payment-related page.
6. Create hourly threshold logic for 404 spikes.
7. Build dashboard panels for URI, status code, and source activity review.

## Skills Demonstrated

| Skill | SOC value |
|---|---|
| Saved report creation | Turns repeated searches into reusable review assets. |
| Source IP aggregation | Identifies high-volume web clients and investigation pivots. |
| Alert-candidate SPL | Documents detection logic without overclaiming full alert deployment. |
| Private IP filtering | Separates internal and external source activity. |
| HTTP status analysis | Supports web troubleshooting, access review, and anomaly detection. |
| Threshold-style aggregation | Builds the foundation for alert tuning and baseline review. |
| Dashboard panel design | Converts raw search results into readable analyst views. |
| Panel title hygiene | Makes dashboards easier to interpret during recurring SOC review. |

## Evidence Map

| Screenshot | What it proves |
|---|---|
| [34-splunk-vpn-logins-by-username-report-search.png](../screenshots/03-splunk-dashboards-and-reports/task-02-reports/34-splunk-vpn-logins-by-username-report-search.png) | Built a reusable VPN login count search by Username. |
| [35-splunk-vpn-logins-by-username-report-view.png](../screenshots/03-splunk-dashboards-and-reports/task-02-reports/35-splunk-vpn-logins-by-username-report-view.png) | Saved the VPN login search as a reusable Splunk report. |
| [36-splunk-web-connections-by-source-ip-report.png](../screenshots/03-splunk-dashboards-and-reports/task-02-reports/36-splunk-web-connections-by-source-ip-report.png) | Reviewed web connections by Source_IP and identified high-volume source activity. |
| [37-splunk-alert-restricted-page-external-sourceip-detection.png](../screenshots/03-splunk-dashboards-and-reports/task-03-alerts/37-splunk-alert-restricted-page-external-sourceip-detection.png) | Built alert-candidate SPL to identify external source IPs accessing `/restricted.html`. |
| [38-splunk-payments-404-total-count.png](../screenshots/03-splunk-dashboards-and-reports/task-03-alerts/38-splunk-payments-404-total-count.png) | Counted total HTTP 404 responses for `/payments.html`. |
| [39-splunk-payments-404-hourly-threshold-rule.png](../screenshots/03-splunk-dashboards-and-reports/task-03-alerts/39-splunk-payments-404-hourly-threshold-rule.png) | Built hourly aggregation logic for `/payments.html` 404 responses. |
| [40-splunk-dashboard-uri-pie-chart-panel.png](../screenshots/03-splunk-dashboards-and-reports/task-04-dashboards/40-splunk-dashboard-uri-pie-chart-panel.png) | Created a dashboard panel visualizing web request distribution by URI. |
| [41-splunk-dashboard-restricted-status-code-table.png](../screenshots/03-splunk-dashboards-and-reports/task-04-dashboards/41-splunk-dashboard-restricted-status-code-table.png) | Created a dashboard panel summarizing response-code distribution for `/restricted.html`. |
| [42-splunk-dashboard-sourceip-uri-statuscode-table.png](../screenshots/03-splunk-dashboards-and-reports/task-04-dashboards/42-splunk-dashboard-sourceip-uri-statuscode-table.png) | Created a dashboard panel summarizing web requests by Source_IP, URI, and status_code. |

## Report and Dashboard Details

| Item | Value |
|---|---|
| VPN report purpose | Recurring review of VPN login volume by user. |
| Web source IP report purpose | Identify high-volume web source IPs for review and pivots. |
| Dashboard title | `Web Logs Overview` |
| Dashboard description | `This dashboard provides an overview of data from the web_logs index.` |
| URI panel title | `URI Distribution` |
| URI content title | `Web Requests by URI` |
| Restricted page panel title | `Restricted Page Status Codes` |
| Restricted page content title | `Restricted Page Response Breakdown` |
| Source summary panel title | `Source, URI, and Status Summary` |
| Source summary content title | `Web Requests by Source IP, URI, and Status` |

## Alert-Candidate Scope

The restricted-page search is documented as alert-candidate SPL. This means the search expresses detection logic that could support alerting, but the artifact does not claim a production alert deployment.

This distinction matters because a strong SOC artifact should separate:

- Search logic
- Dashboard logic
- Alert-candidate logic
- Production alert lifecycle and tuning

## Analyst Notes

Reports help standardize repeated review. Dashboards help reduce cognitive load by grouping relevant panels in one place. Alert-candidate searches help document detection thinking before formal deployment.

The restricted-page search demonstrates an important SOC pattern: do not only search for a sensitive URI. Add context. In this case, private IP ranges are excluded so the analyst can focus on external source IPs accessing a restricted resource.

The payment-page 404 workflow demonstrates threshold thinking. Counting total errors is useful, but hourly aggregation gives better context for spikes and alert tuning.

## Related SPL

See:

[03-reports-alerts-dashboards.spl](../spl/03-reports-alerts-dashboards.spl)
