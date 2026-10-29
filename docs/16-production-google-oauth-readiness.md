# 16 — Production Google OAuth Readiness and Verification

**Date:** 2026-10-30  
**Purpose:** Verify real Google sign-in on the selected production/live environment without confusing environment selection with working authentication.  
**Status:** Readiness checklist; not proof of a successful live integration.

## 1. Current known state

The owner reports that the relevant environment was changed from “level 4” to production/live so Google access can be used. The exact platform/project, production origin, deployed commit, OAuth client configuration, consent-screen state, and end-to-end test result have not been independently verified by this documentation change.

Use these distinct status labels:
- **Environment selected:** production/live selected in the relevant platform.
- **Configuration complete:** origin, callback, OAuth client, consent screen, and secrets configured.
- **OAuth verified:** sign-in and callback/session lifecycle pass on the real production origin.
- **Customer journey verified:** OAuth, onboarding, one-time grant, generation, and private result delivery all pass.
- **Production-ready:** required security, privacy, reliability, cost, rollback, and acceptance gates pass.

Never use one label as proof of another.

## 2. Required configuration inventory

Record these values in the project’s secure operations record. Do not place secret values in this document or Git.

| Item | Required evidence |
|---|---|
| Hosting/auth platform | Platform name and environment/project identifier |
| Production origin | Exact HTTPS origin |
| Deployed version | Commit SHA/build ID and deployment timestamp |
| Google Cloud project | Correct project selected for the OAuth client |
| OAuth client type | Appropriate web application client for the architecture |
| Authorized JavaScript origins | Exact production origin(s) only, where required |
| Authorized redirect URIs | Exact callback URL emitted by the chosen auth framework |
| Consent screen | Audience, app name, support contact, privacy policy, requested scopes and status |
| Secret storage | Client secret stored in platform secret manager, never Git |
| Auth framework | Library/provider route and documented callback path |
| Test evidence | Date, browser/device, scenario, observed result, sanitized log reference |

Do not guess callback URLs. Obtain the exact callback URL from the actual authentication library/platform configuration and register that exact URI with Google.

## 3. Google OAuth configuration workflow

1. Identify the exact application and hosting project intended to serve production traffic.
2. Confirm that the selected environment deploys the intended application and commit; verify the actual HTTPS origin.
3. In the correct Google Cloud project, inspect the OAuth consent configuration and OAuth client. Ensure the client type matches the application.
4. Add only the exact authorized origins and redirect URIs required by the application. Avoid wildcard redirects and unnecessary origins.
5. Confirm the app’s audience and publishing/testing status. If the app is restricted to test users, verify the intended test account is included. If public use is intended, complete applicable consent-screen and verification requirements before claiming unrestricted access.
6. Request the minimum necessary scopes. Basic sign-in should not request Drive, YouTube, or other APIs unless a separate approved feature genuinely needs them.
7. Add the client ID and any required secret through the production platform’s secret/environment settings. Never expose a client secret in frontend code, logs, screenshots, commits, or chat.
8. Confirm the auth framework’s production callback, cookie/session configuration, and trusted origin settings.
9. Redeploy/restart if the platform requires it, then run the tests below on the actual production origin.
10. Record sanitized evidence and the exact deployed commit. Do not report success based solely on a successful build or the appearance of a Google button.

## 4. End-to-end verification matrix

| ID | Scenario | Expected result |
|---|---|---|
| G-01 | New user selects “Continue with Google” | Google sign-in flow opens on the expected origin |
| G-02 | Valid consent and callback | User returns to the intended app route with a valid session |
| G-03 | Returning user signs in | Existing internal account is resolved using stable provider subject |
| G-04 | User cancels or denies consent | Clear recoverable state; no false success and no free grant |
| G-05 | Callback has invalid state/nonce or wrong audience/issuer | Request rejected safely |
| G-06 | Redirect URI mismatch | Error is surfaced safely; no insecure fallback |
| G-07 | Session refresh/expiry | Session behaves according to documented expiry policy |
| G-08 | Logout | Session is invalidated and protected pages require sign-in |
| G-09 | Duplicate callback/retry | No duplicate internal user or entitlement grant |
| G-10 | Two accounts attempt to access one another’s resources | Access is denied |
| G-11 | Google or auth provider is unavailable | Safe failure state; no grant/job duplication |
| G-12 | Inspect application logs | No OAuth code, token, client secret, or unnecessary personal data exposed |

A passing test must include an observed result, date, environment/origin, and deployed commit/build identifier. A checklist tick without evidence is not verification.

## 5. Identity and privacy rules

- Use the stable provider subject (`sub` or equivalent verified provider identifier) as the external identity key; do not use email as the sole account key.
- Treat email and profile fields as claims returned by Google. Request only what the sign-in flow needs and disclose processing in the privacy notice.
- Validate OAuth state/nonce and issuer/audience using the selected auth library/provider.
- Do not store access/refresh tokens unless a separately approved feature requires them.
- Use secure, HttpOnly, appropriately SameSite cookies and HTTPS. Set session lifetime and logout behavior deliberately.
- Avoid logging callback query strings, authorization codes, tokens, or full identity payloads.
- Provide a practical way to contact the operator about account access/deletion, and document retention before opening public registration.

## 6. Connection to the one-time free generation

Google sign-in success alone must not trigger client-controlled quota logic. After a verified identity is established:

1. Upsert the internal user using the provider subject.
2. Create the initial entitlement once using a server-side unique/idempotency constraint.
3. On every generation request, verify the session, entitlement, request limits, provider status, and cost policy server-side.
4. Create/reserve the job and entitlement atomically, or keep generation disabled until safe atomicity is available.
5. Deliver assets only to the owner through authenticated access or short-lived authorized URLs.
6. Ensure OAuth callback retries, browser refreshes, and duplicate requests cannot issue multiple free grants or generation jobs.

If the generation provider or its real cost is unknown, Google login may be tested separately, but generation must remain disabled or clearly marked as a non-production demo.

## 7. Go/no-go decision

**GO for OAuth testing** only when the actual production origin, OAuth client, redirect URI, secret storage, and test-account/audience setup are identified.

**GO for public sign-in** only when end-to-end sign-in, callback/session security, error cases, privacy disclosure, abuse protection, and support/deletion handling pass.

**GO for free generation** only when one-time entitlement enforcement, provider execution, cost caps, idempotency, failure recovery, and private asset authorization pass.

**NO-GO** if any callback URI is guessed, a secret is exposed, accounts can access other users’ data, quota can be duplicated, provider cost is unbounded/unknown, or a mock output is presented as a real generated asset.

## 8. Evidence record template

- Environment/project:
- Production origin:
- Deployed commit/build:
- OAuth client identifier (non-secret label only):
- Authorized redirect URI:
- Consent/audience status:
- Test date and browser/device:
- Test IDs passed:
- Test IDs failed:
- Sanitized evidence/log reference:
- Known limitations:
- Rollback/disable procedure:
- Reviewer/owner decision:

Do not include client secrets, tokens, authorization codes, full ID tokens, or other credentials in this record.
