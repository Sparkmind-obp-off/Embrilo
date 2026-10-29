# 15 — Self-Service Product Metrics and Privacy-Safe Events

## North Star

For self-service, use **Successful First Generations (SFG)**: distinct eligible users receiving at least one usable output from a completed generation job in the reporting period. Exclude mocks, demos, failures and duplicate events.

Keep Qualified Deliveries Accepted (QDA) for the separate human-assisted service. Do not combine the metrics.

## Funnel events

landing_view; onboarding_started; onboarding_completed; google_auth_started; google_auth_succeeded; free_grant_created; generation_submitted; generation_started; generation_succeeded; generation_failed; asset_downloaded; repeat_generation_requested.

Record only minimum necessary fields: event ID, timestamp, pseudonymous internal user ID where appropriate, event name, output type, job ID, status/error code and environment. Never send OAuth tokens, email addresses, raw prompts, private asset URLs or file contents to analytics.

## Metrics

- Onboarding completion = completed / started.
- Google sign-in success = succeeded / started.
- First-generation activation = users with successful first generation / users with grant.
- Generation success = successful jobs / accepted jobs.
- Median and p95 time to usable output.
- Provider failure and retry rates.
- Estimated/actual cost per successful generation.
- Free-grant utilization, repeat use and abuse/rate-limit events.

Set no numerical target before baseline data exists. Measure a small preview cohort first.

## Instrumentation rules

Emit trusted lifecycle events server-side; deduplicate with stable event/job IDs; separate development, preview and production data; apply retention/access controls; document deletion/anonymization. Analytics must not be the source of truth for quota or billing; use transactional records.
