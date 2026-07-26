---
name: Register and verify Diligent webhooks
description: Register a signed webhook endpoint, subscribe to Diligent events, and verify and redeliver deliveries.
api: openapi/diligent-openapi-original.json
operations:
  - registerWebhook
  - listWebhooks
  - listWebhookDeliveries
  - redeliverWebhook
---

# Register and verify Diligent webhooks

Authenticate with the `X-API-KEY` header.

## Steps

1. **Register** — `registerWebhook` (`POST /webhooks`) with `webhook_url` (must be
   HTTPS), a `secret` used to sign payloads, and the `events` to subscribe to.
   Available events: `cdd_state_changed`, `monitoring_alert_fired`.
2. **Verify signatures** — every delivery is signed with your shared secret and
   sent in the `X-Signature` header. Recompute the signature over the raw body
   and compare before trusting the payload
   (see `guides/webhooks/securing-webhooks`).
3. **List / inspect** — `listWebhooks` (`GET /webhooks`) to see registered
   endpoints; `listWebhookDeliveries` (`GET /webhooks/{webhook_id}/events`) to
   review recent deliveries.
4. **Redeliver** — `redeliverWebhook`
   (`POST /webhooks/{webhook_id}/events/{event_id}/redeliver`) to replay a missed
   or failed event.

## Rules

- Only HTTPS `webhook_url` values are accepted.
- Always verify `X-Signature` before acting on a payload.
