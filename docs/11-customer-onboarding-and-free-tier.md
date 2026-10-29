# 11 — Customer Onboarding, Google Sign-In, and Free Generation

**Status:** Development specification only; not proof of implementation or production readiness.
**Priority:** P0. Development/preview first.

## Product decision

The first self-service journey is visitor → onboarding → Google sign-in/sign-up → one-time free generation grant → generator → result/history → next-step guidance. Keep the human-assisted service workflow as a separate path.

Email/password registration is not part of the initial signup UI. Google OAuth may return an email as an identity-provider claim; do not promise that no email data is processed. Request only necessary scopes and explain profile data use in the privacy notice.

## Customer journey and routes

1. Public landing page explains supported outputs, limits, and a clear “Coba gratis” CTA.
2. Onboarding asks only useful basics: goal, output type, platform. Provide defaults and let optional questions be skipped.
3. Sign-in gate offers “Lanjutkan dengan Google” and preserves the intended destination across OAuth redirect.
4. First-login provisioning upserts an internal user from verified identity and grants one free entitlement idempotently.
5. Workspace shows the server-derived remaining allowance and only output modes with a verified provider path.
6. Generation form captures prompt/brief, supported format, explicit limits, and rights confirmation where relevant.
7. Submission validates session, schema, abuse limits, entitlement, provider availability, and cost policy. Reserve the entitlement and create one idempotent job atomically.
8. Job status shows queued, processing, completed, or failed. No status endpoint may reveal another user's data.
9. Result supports owner-authorized preview/download and records asset metadata.
10. After use, show history, limits, and truthful next steps. Paid plans and checkout remain disabled until explicitly approved and tested.

Returning users resume their workspace. OAuth cancellation or provider errors must not show false success.

## Free entitlement policy

- One free generation grant per internal user account.
- Grant is created server-side and idempotently; never trust a client-supplied user ID or balance.
- A generation means one accepted job producing one primary output within documented format, duration, resolution, and cost limits.
- Reserve the grant atomically when a valid job is accepted. Duplicate requests with the same idempotency key return the existing job.
- For confirmed provider/system failure before usable output, release the reservation exactly once according to documented failure policy. Refreshing the page does not restore a used grant.
- Successful generation consumes one grant. Maintain an append-only ledger.
- Apply per-account rate limits and abuse controls. Do not rely on cookies/local storage as entitlement enforcement.
- One account per person cannot be perfectly guaranteed without proportionate identity controls. Avoid invasive fingerprinting and unnecessary sensitive data collection.
- If provider capability or cost is unverified, disable that mode or offer a clearly labelled manual/demo fallback. Never imply a real video was generated if only a script/mock preview exists.

## Suggested data model

- users: id, auth_provider, provider_subject unique, display_name nullable, email nullable, email_verified nullable, created_at, updated_at, deleted_at nullable.
- onboarding_profiles: user_id unique FK, goal, preferred_output_type, preferred_platform, completed_at, updated_at.
- entitlements: id, user_id, grant_type, granted_units, policy_version, created_at, idempotency_key unique.
- credit_ledger: id, user_id, entitlement_id, job_id nullable, event_type (grant/reserve/consume/release/adjustment), units_delta, idempotency_key unique, reason_code, created_at. Append-only.
- generation_jobs: id, user_id, idempotency_key, output_type, validated_request_json, status, provider, provider_job_id nullable, reserved_units, error_code nullable, created_at, started_at nullable, finished_at nullable, updated_at.
- assets: id, job_id, user_id, storage_key, media_type, size_bytes nullable, checksum nullable, status, created_at, expires_at nullable.
- audit_events: id, actor_type, actor_id nullable, event_type, target_id nullable, safe_metadata_json, created_at.
- provider_usage: id, job_id, provider, model_or_feature nullable, units nullable, estimated_cost_minor nullable, actual_cost_minor nullable, currency, recorded_at, source (measured/estimated/unknown).

Use migrations and foreign keys. Index users by provider subject; jobs by user and creation time/status; assets by user/job; ledger by user and creation time. Never store OAuth tokens unless a necessary integration is separately designed and secured.

## API contract (adapt to actual stack)

- GET /api/me — authenticated minimal profile, onboarding state, and derived entitlement.
- PUT /api/onboarding — authenticated, validated profile upsert.
- GET /api/generations — authenticated, paginated jobs owned by user.
- POST /api/generations — authenticated; requires Idempotency-Key; validates output, limits, rights and entitlement.
- GET /api/generations/:id — owner-only status and safe error state.
- GET /api/assets/:id/download — owner-only short-lived access or authenticated streaming; never expose private bucket keys.
- GET /api/health — minimal non-sensitive health information.
- Use the chosen auth library's OAuth/session routes rather than inventing a callback implementation.

Use a database transaction or safe conditional writes to reserve the grant and create the job. If atomicity cannot be guaranteed, do not enable generation.

## Provider adapter and cost safety

Define capability discovery, submit, status lookup, result retrieval, and normalized errors. Keep credentials server-side. Mark cost as measured, estimated, or unknown. Configure maximum jobs, concurrency, output limits, and daily spend. Default to disabled when a hard budget guard cannot be enforced. Retry only transient failures and use provider idempotency when available.

## Security and privacy

Verify OAuth state/nonce and issuer/audience through the auth provider. Enforce authorization on every API and asset request. Validate input server-side, limit request/upload sizes, and inspect actual file types. Treat prompts and uploaded text as untrusted input. Apply CSRF protection where required, secure HttpOnly/SameSite cookies, sensible session expiry, rate limits, and safe logs. Define retention/deletion and explain OAuth profile use before launch. Keep secrets in provider secret storage. Use private object storage and owner checks before short-lived signed URLs. Never expose stack traces or secrets to customers.

## UX states

Design loading, success, empty, validation error, OAuth cancellation, expired session, quota unavailable, queued/processing, provider timeout, generation failure, result expired, and network failure. Preserve safe form input on recoverable errors.

## Acceptance tests

1. New Google user gets one internal user and one grant.
2. Existing Google user receives no extra grant.
3. OAuth cancel/failure creates no usable session or grant.
4. Onboarding can be completed and resumed.
5. Unauthenticated generation calls are rejected.
6. User A cannot view/download User B's job or asset.
7. Duplicate idempotency key creates one job and reservation.
8. Concurrent requests cannot spend one grant twice.
9. Successful output consumes exactly one unit.
10. Eligible failure releases reservation exactly once.
11. Unknown provider cost does not trigger uncontrolled retries.
12. Rate and payload limits work.
13. UI states are accessible and clear.
14. Logs/Git contain no secrets or unnecessary personal data.
15. UI matches server entitlement; inactive checkout is not presented as usable.

## Release gates

Stay in development/preview until OAuth is verified, real provider generation is demonstrated end-to-end, cost limits and failure semantics pass, cross-account authorization passes, privacy/retention copy is approved, migrations and backup/restore are tested, and domain/HTTPS checks pass. Unit-test counts alone are insufficient.

## Production environment note (2026-10-30)

The owner reports switching the relevant environment from “level 4” to production/live to enable real Google access. The environment change itself does not prove that Google OAuth works end to end. Before relying on it, complete `docs/16-production-google-oauth-readiness.md` and record the exact origin, redirect URI, deployed commit, and test evidence. Keep the free-generation grant and provider execution disabled until server-side quota enforcement, provider access/cost, and private asset access are verified.
