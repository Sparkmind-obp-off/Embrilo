# 13 — Onboarding and Free Generation Test Plan

Use development/preview auth, synthetic users, non-sensitive prompts, and a provider mode with known cost. Do not run billable generation without an owner-approved cap. Never commit test credentials.

| ID | Scenario | Expected result |
|---|---|---|
| T-01 | New Google user | Valid session, one internal user, one grant |
| T-02 | Existing user signs in again | Same internal user; no extra grant |
| T-03 | User cancels OAuth | Recoverable message; no grant |
| T-04 | Invalid OAuth state/nonce | Rejected safely |
| T-05 | Partial onboarding | Safe fields persist; user can resume |
| T-06 | Completed onboarding | Workspace opens with accurate entitlement |
| T-07 | Unauthenticated generation request | Rejected; no job |
| T-08 | Invalid output or oversized payload | Validation error; no reservation |
| T-09 | Same idempotency key repeated | Same job; one reservation |
| T-10 | Concurrent requests with one free unit | At most one accepted job |
| T-11 | Provider succeeds | One usable asset; grant consumed once |
| T-12 | Provider fails before usable output | Safe error; eligible release happens once |
| T-13 | Refresh during processing | Existing job shown; no duplicate job |
| T-14 | Timeout/unknown provider status | No uncontrolled billable retry |
| T-15 | User A requests User B's job | Denied without revealing private details |
| T-16 | User A requests User B's asset | Access denied; no signed URL leaked |
| T-17 | High-rate malformed requests | Rate limited; service remains stable |
| T-18 | Provider unavailable | Mode disabled or honest fallback; no false success |
| T-19 | Cost unknown | Guard prevents unbounded generation |
| T-20 | Logs inspected | No secrets, tokens, signed URLs, or unnecessary prompt data |
| T-21 | Mobile keyboard use | Controls, focus, labels and errors accessible |
| T-22 | Deletion/retention request | Documented deletion/anonymization procedure |
| T-23 | Free allowance displayed | UI matches server-derived state |
| T-24 | Checkout not configured | No misleading active purchase flow |

For every run record test ID, environment, app commit, date, expected/observed result, pass/fail and redacted evidence location. Do not alter expected results merely to make tests pass.

All P0 tests must pass in preview. Cross-account access, double-spend, and uncontrolled-cost failures block release. Production is a separate decision after privacy, operations, rollback, and domain checks.
