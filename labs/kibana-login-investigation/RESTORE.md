# Restoring the Kibana Lab

The saved objects were exported from Kibana **9.5.5**. Use the same version for the closest match. The export contains dashboard configuration and a data view; the simulated events are supplied separately in `data/sample-login-events.ndjson`.

## Import data

1. Start a local Elasticsearch and Kibana environment.
2. Create index `learning-auth` using the mappings in `data/index-mapping.json`. In Kibana Developer Tools, use `PUT learning-auth` with that JSON as the request body. If the index already exists, inspect its mappings and contents before making changes.
3. Import `data/bulk-login-events.ndjson` using the Elasticsearch Bulk API (`POST /_bulk?refresh=true`, content type `application/x-ndjson`) and your local authentication credentials. It already includes action lines and stable IDs, so reloading the same fixture does not create duplicates. Alternatively, paste its contents after `POST _bulk?refresh=true` in Kibana Developer Tools. The example below shows the first action/document pair. The ordinary event file `sample-login-events.ndjson` does not include action lines.

```text
POST _bulk?refresh=true
{"index":{"_index":"learning-auth","_id":"0"}}
{"@timestamp":"2026-10-15T17:25:11.566766+00:00","event":{"category":["authentication"],"action":"user_login","outcome":"failure","dataset":"learning.authentication"},"user":{"name":"taylor"},"source":{"ip":"192.0.2.10"},"host":{"name":"practice-laptop"},"message":"Synthetic login event for learning"}
```

## Import dashboard

1. Open **Stack Management → Saved Objects → Import**.
2. Select `exports/dashboard.ndjson`. This includes the related chart definitions and data view with ID `learning-auth`.
3. If Kibana reports existing objects, review the conflicts before choosing whether to overwrite them.
4. Open **Dashboards → Login Security Overview**.
5. Confirm the saved date range is October 15–16, 2026. Use October 15 at 00:00 UTC through October 17 at 00:00 UTC if you need a wider range. Relative ranges such as Last 15 minutes will exclude these events.

## Validate

- The index contains 680 events and the failure query returns 183.
- The account chart shows 104 failures for `alex`.
- The source chart shows 80 failures for `203.0.113.50`.
- Reopening the dashboard preserves all three panels and its date range.

The export was checked for one dashboard, three Lens visualizations, and one data view. A fresh-instance restore has not been tested.
