# Top 3 triggered detections last 14 days

## Overall detections

This query doesn't distinct between the built-in and your custom detections.

```text
let starttime = ago(14d);
let endtime = ago(1h);

Alertinfo
| where TimeGenerated btween(starttime..endtime)
| summarize Count=count() by Title
| sort by Count desc | top 3 by Count
| render piechart(title="Top 3 incidents by title")
```

## Custom detections

This query does distinct between the built-in and your custom detections. Since custom detections are easier to tune since you know exactly what the code is, it is recommended to start working on your custom detections first.

```text
let starttime = ago(14d);
let endtime = ago(1h);

AlertEvidence
| where TimeGenerated btween(starttime..endtime)
| where DetectionSource contains @"custom" or DetectionSource contains @"NRT"
| summarize Count=count() by Title
| sort by Count desc | top 3 by Count
| render piechart(title="Top 3 incidents by title")
```
