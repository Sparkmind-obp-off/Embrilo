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

Embrilo helps a customer turn a clear brief into content assets through AI-assisted drafting and production, followed by human review and delivery. The exact deliverable types and scope are selected per offer and must be stated before payment.

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
- Whether the first web MVP needs authentication or can use a simple intake form.
- Domain DNS records and hosting configuration.

## Change control

Any change to locked decisions must be recorded in this document with date, reason, impact, and owner approval. Never silently change the brand name, stack, budget principle, or production scope.
