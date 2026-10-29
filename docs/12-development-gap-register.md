# 12 — Development Gap Register and Release Gates

**Reviewed:** 2026-10-29. Based on repository documents and owner-provided development context. Items marked unverified require runtime evidence.

## Evidence rules

Specified means written in docs. Reported means development notes say it exists. Verified means directly tested with repeatable evidence in the target environment. Never promote specified/reported to verified without test evidence, a commit, a redacted log, or a reproducible result.

| ID | Area | Current evidence | Required action | Priority | Exit evidence |
|---|---|---|---|---|---|
| G-01 | Actual app source | Repository tree is documentation/templates focused | Identify the real app repository and deployed commit | P0 | Commit SHA and source paths |
| G-02 | Google auth | Google/Clerk reported, not verified in this audit | Verify provider settings, redirects, state/nonce, sessions, preview/prod separation | P0 | New, returning, cancelled login tests |
| G-03 | Customer journey | Original PRD centers on service brief intake | Implement visitor → onboarding → Google → grant → generator → result | P0 | End-to-end evidence |
| G-04 | Free grant | Not in original service-oriented schema | Server-side idempotent grant and ledger | P0 | Repeat-login/concurrency tests |
| G-05 | Generation adapter | Existing bridge explicitly manual/design-only | Verify provider access, limits, cost and real output; otherwise label fallback | P0 | Output and provider/cost evidence |
| G-06 | Job lifecycle | Runtime not verified | Job states, idempotency, timeout, retry and normalized errors | P0 | Success/failure/timeout tests |
| G-07 | Asset privacy | Private storage recommended, not verified | Owner checks and secure delivery | P0 | Cross-account access tests |
| G-08 | Free-tier economics | Cost principle documented, budget not quantified | Output caps, cost estimate, daily cap, disable-on-unknown policy | P0 | Cost worksheet and tested guard |
| G-09 | Schema | Original schema focuses clients/projects | Add users, onboarding, entitlements, ledger, jobs, assets and usage as needed | P0 | Migration and restore evidence |
| G-10 | Privacy/retention | General principles exist | Document Google profile fields, purpose, retention, deletion and AI-provider processing | P1 | Owner-approved notice |
| G-11 | Abuse controls | Generic spam controls recommended | Rate limits, payload/concurrency limits and monitoring | P1 | Abuse tests |
| G-12 | UX/accessibility | Design direction exists | Test OAuth errors, quota states, job failure, keyboard and mobile | P1 | QA checklist |
| G-13 | Analytics | Existing North Star is paid accepted service deliveries | Add activation and successful-generation metrics separately | P1 | Event specification and privacy review |
| G-14 | Docs consistency | Docs reflect service-first model | Sync PRD, architecture, schema, UI/UX, roadmap, QA, README and master prompt | P0 | Cross-document review |
| G-15 | Release process | QA checklist exists; deployment evidence not reviewed | Preview gate, rollback, backup, domain/HTTPS and release note | P1 | Reproducible release record |

## Recommended order

1. Identify actual app source and deployed commit.
2. Verify Google OAuth/session behavior in development.
3. Implement onboarding and one-time server-side entitlement.
4. Implement idempotent job lifecycle and provider adapter with cost controls.
5. Verify real output and private asset access.
6. Add failure, abuse, and accessibility tests.
7. Sync docs and prepare release evidence.
8. Do not enable production generation or paid plans until P0 gates pass.

## Definition of done

A feature is done only when implementation exists, automated tests actually run, critical acceptance tests pass in preview, failure modes are covered, and docs match behavior. Build passing is not equivalent to feature working; deployed is not equivalent to production-ready.
