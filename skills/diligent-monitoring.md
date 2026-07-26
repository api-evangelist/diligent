---
name: Set up ongoing monitoring and handle alerts
description: Create monitoring configurations for customers and process the alerts they raise using the Diligent API.
api: openapi/diligent-openapi-original.json
operations:
  - "POST /monitorings"
  - "POST /monitorings/bulk-create"
  - "GET /monitorings"
  - "GET /monitoring-alerts"
  - "POST /monitoring-alerts/acknowledge"
  - "DELETE /monitorings/{id}/deactivate"
---

# Set up ongoing monitoring and handle alerts

Authenticate with the `X-API-KEY` header.

## Steps

1. **Create monitoring** — `POST /monitorings` to create a single monitoring
   configuration for a customer (alerts on website changes and risks), or
   `POST /monitorings/bulk-create` for up to 200 in one request.
2. **List monitorings** — `GET /monitorings` to page through the active
   configurations (`page_size` query param).
3. **Read alerts** — `GET /monitoring-alerts` to retrieve raised alerts. Or
   register a webhook for the `monitoring_alert_fired` event to be notified
   instead of polling.
4. **Acknowledge alerts** — `POST /monitoring-alerts/acknowledge` to mark one or
   all alerts as seen.
5. **Deactivate** — `DELETE /monitorings/{id}/deactivate` to stop a monitoring.
   This operation is idempotent and safe to repeat.

## Rules

- Errors use the custom `error` / `errors[]` envelope
  (see `errors/diligent-problem-types.yml`).
