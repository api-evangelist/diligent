---
name: Perform a Customer Due Diligence (CDD) case
description: Run a CDD check on a business, attach documents, run risk checks, and download the report using the Diligent API.
api: openapi/diligent-openapi-original.json
operations:
  - "POST /cdds"
  - "GET /cdds/{id}"
  - "POST /cdds/{id}/documents"
  - "POST /cdds/{id}/run-checks"
  - "GET /cdds/{id}/report"
---

# Perform a Customer Due Diligence (CDD) case

Authenticate every request with the `X-API-KEY` header. Use the sandbox host
`https://api.sandbox.godiligent.ai` for testing and `https://api.godiligent.ai`
for production.

## Steps

1. **Create the case** — `POST /cdds` with the business identity in the request
   body (legal name + address, register number + country code, or website).
   Send an `idempotency-key` header so safe retries don't create duplicate cases;
   reusing a key with a different payload returns `409 Conflict`.
2. **Poll the case** — `GET /cdds/{id}` until its state reaches `complete` or
   `inconclusive`. Instead of polling, register a webhook for the
   `cdd_state_changed` event (see the webhooks skill).
3. **Attach documents (optional)** — `POST /cdds/{id}/documents` to add supporting
   documents, or `POST /cdds/{id}/pull-registry-documents` to pull official
   registry filings (supported in IT and DE only).
4. **Run risk checks (optional)** — `POST /cdds/{id}/run-checks` to run (or re-run)
   the risk checks on a completed case.
5. **Get the report** — `GET /cdds/{id}/report` to download the detailed CDD report.

## Rules

- Concurrency limit: 10 concurrent CDD cases per account.
- Errors return a custom envelope: an `error` string, or an `errors[]` array for
  validation failures (see `errors/diligent-problem-types.yml`).
