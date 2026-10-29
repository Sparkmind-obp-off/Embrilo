# 14 — Free-Tier Cost and Capability Guardrails

**Status:** Policy template. No provider pricing or free allowance is assumed verified.

## Principle

A free allowance is a product promise and a cost exposure. Enable only modes whose access, limits, rights, latency, and marginal cost are known well enough to cap safely.

## Capability registry

For each mode record output type; provider/feature; official documentation or verified account evidence; authentication and plan eligibility; maximum duration/resolution/size/output count; expected and actual cost per successful job; rate/concurrency limits; timeout behavior; retention, rights and watermarking; fallback and kill switch; last verified date and owner.

If an essential field is unknown, mark the mode disabled or manual-only. A provider's web UI does not prove a public API exists.

## Cost calculations

Expected cost per accepted job = generation cost + storage/egress estimate + retry allowance + other metered services.

Worst-case daily exposure = maximum accepted jobs per day × configured maximum cost per job.

Use actual provider rates and observed usage, not invented prices. Use a conservative upper bound for variable costs. If no defensible upper bound exists, do not expose automated generation to free users.

## Initial rules

- One grant per internal account; one primary output per grant.
- One in-flight job per account by default.
- Strict request, body, upload and output limits.
- Per-account rate limits and global concurrency cap.
- Server-side daily budget ceiling and emergency kill switch.
- No automatic retries of potentially billable jobs unless idempotency and billing semantics are known.
- No silent switch to a higher-cost provider.
- No automatic public publishing.
- Minimize and redact prompt data in logs.

Embrilo-funded trial usage is not necessarily a provider-funded free tier. Tell users what is included and that availability may be constrained during development.

Review before enabling a new mode, after provider-plan changes, and after unexpected bills. If access or cost becomes uncertain, disable the mode until re-verified.
