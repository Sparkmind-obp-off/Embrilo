# 00 — Embrilo Source of Truth

**Version:** 0.1.0  
**Updated:** 2026-10-27  
**Status:** Initial decisions; not yet market-validated.

## Locked decisions

- Brand name: **Embrilo**. Do not restart naming exploration unless the owner explicitly requests it.
- Domain purchased by owner: **embrilo.biz.id**. Registration is owner-reported; DNS and production deployment are not verified here.
- Repository: `Sparkmind-obp-off/Embrilo`.
- Business direction: AI-assisted content production with human quality control.
- Initial market/language: Indonesian customers; Indonesian is the default language.
- Budget principle: minimize additional cash spend; prefer free tiers and manual workflows until there is evidence to automate.
- Build philosophy: service-first, evidence-led, modular, secure, and simple.

## Current state

| Area | State |
|---|---|
| Brand direction | Decided |
| Domain | Owner reports purchased |
| GitHub repository | Exists; this repository is the documentation source of truth |
| Service offer | Proposed, not validated |
| Pricing | Not decided; research and cost model required |
| Portfolio | No real client work confirmed |
| Website | Not verified as built or deployed |
| Genspark production bridge | Specified in documentation; not connected or live |
| Payments | Not configured or verified |
| AI workflow | Proposed; requires manual test runs |
| Database / application | Not implemented or verified |
| Customer demand / revenue | No evidence supplied in this project context |

## Product definition

Embrilo has two distinct paths: (1) self-service product journey: visitor → short onboarding → Google sign-in/sign-up → one-time free generation grant → supported generator → secure result; and (2) optional human-assisted content production with scoped briefs, human QC, and delivery. Do not force self-service users into a paid-service intake form.

## Self-service MVP decisions (2026-10-29)

- Google OAuth is the only signup UI for the initial self-service MVP; no separate email/password form. Google may return an email claim, which must be disclosed and minimized.
- A newly eligible internal user receives one free generation grant, created server-side and idempotently.
- Generation quota is controlled through a server-side ledger and job lifecycle; duplicate requests must not double-consume or double-generate.
- Provider capability, access, output limits and cost must be verified before a generation mode is enabled.
- Development/preview first. No production readiness claim without repeatable evidence.
- Paid checkout, subscriptions, autonomous publishing and unverified API bridges remain disabled.

## Principles

1. **Truth over polish:** no fabricated customers, testimonials, performance claims, market statistics, or portfolio credentials.
2. **Human approval:** generated work is a draft until checked against the brief and quality rubric.
3. **Evidence labels:** distinguish verified fact, observed source, inference, hypothesis, and unknown.
4. **Cost awareness:** do not activate paid services, paid APIs, or subscriptions without a specific justified need.
5. **Integration honesty:** a designed bridge is not a live integration; test and document each connection.
6. **Least privilege:** secrets belong in provider secret stores or local ignored environment files, never in Git.
7. **Customer trust:** clarify scope, revision limits, deadlines, usage rights, and dependencies before accepting payment.
8. **No premature SaaS:** manually deliver the first service before building complex self-service automation.

## Decisions still open

- First target niche and buyer persona.
- First single, tightly scoped offer and price.
- Exact supported content formats and output quantities.
- Preferred Genspark features available in the owner's current plan.
- Payment method and production payment verification.
- Public contact method and customer support policy.
- Actual application repository and deployed commit to audit.
- Verified Google OAuth/session configuration.
- Supported generation provider, real capability, cost limits and fallback.
- Entitlement ledger, generation-job lifecycle and private asset delivery implementation.
- Privacy notice, retention/deletion policy and preview acceptance evidence.
- Domain DNS records and hosting configuration.

## Change control

Any change to locked decisions must be recorded in this document with date, reason, impact, and owner approval. Never silently change the brand name, stack, budget principle, or production scope.
