---
name: Remediate a name-screening alert
description: Submit an externally-screened sanctions/PEP alert to Diligent for AI-powered remediation and entity resolution.
api: openapi/diligent-remediation-openapi.json
operations:
  - "POST /v1/name-screenings/alerts/remediate"
---

# Remediate a name-screening alert (Beta)

The Remediation API (Beta, v0.1.0) automates the review of false-positive alerts
from an external sanctions/PEP screening provider. Authenticate with the
`X-API-KEY` header. Base host: `https://api.godiligent.ai` (or
`https://api.sandbox.godiligent.ai` for testing).

## Steps

1. **Submit the alert** — `POST /v1/name-screenings/alerts/remediate` with the
   externally-screened alert (the subject you screened plus the candidate hits
   returned by your screening provider).
2. **Read the AI remediation** — the response returns the AI-powered entity
   resolution and remediation decision (match / no-match with supporting
   evidence) so your compliance analysts can clear false positives faster.

## Rules

- This is a Beta surface; shapes may change.
- Concurrency limit: 20 concurrent name-screening requests per account.
- See `guides/name-screening/remediation-api` in the Diligent docs for the full
  request/response contract.
