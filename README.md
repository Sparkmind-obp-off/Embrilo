# Embrilo

**Brand:** Embrilo  
**Domain:** https://embrilo.biz.id  
**Repository:** https://github.com/Sparkmind-obp-off/Embrilo  
**Status:** Documentation-first foundation; implementation and live integrations are not yet verified.

Embrilo is an AI-assisted content production service with human quality control. The first goal is to validate and deliver a small, paid service reliably—not to build a complex SaaS platform before demand exists.

## Start here

1. [Source of Truth](docs/00-source-of-truth.md) — locked decisions, assumptions, and guardrails.
2. [Master Business Blueprint](docs/01-master-business-blueprint.md) — customer, offer, delivery model, and validation.
3. [Content Operating System](docs/02-content-operating-system.md) — content strategy, brief, production workflow, and QC.
4. [AI Production Bridge](docs/03-ai-production-bridge.md) — human-controlled handoff between briefs, Genspark, review, and delivery.
5. [Product Requirements (PRD)](docs/04-prd.md) — user journeys, MVP requirements, and acceptance criteria.
6. [Technical Architecture](docs/05-technical-architecture.md) — deployment and integration boundaries.
7. [Database Blueprint](docs/06-database-blueprint.md) — initial data model and migration approach.
8. [UI/UX Specification](docs/07-ui-ux-specification.md) — pages, design system, and accessibility.
9. [MVP Roadmap and Metrics](docs/08-mvp-roadmap-and-metrics.md) — phases, North Star, and go/no-go gates.
10. [Genspark Master Prompt](docs/09-genspark-master-prompt.md) — execution instructions for Genspark.
11. [Operations and QA](docs/10-operations-and-qa.md) — production checklists, safety, tests, and delivery.

## Build order

**First:** validate one small content offer and run the workflow manually.  
**Second:** standardize the brief, prompt templates, quality rubric, and delivery pack.  
**Third:** build a lightweight public website and internal project tracker.  
**Later:** automate integrations only after their access, cost, reliability, and customer value are verified.

## Important status rule

A document or specification is not an implemented feature. Do not claim the site is deployed, a payment is connected, an AI bridge is live, or tests have passed unless evidence confirms it. Keep credentials out of Git.


## Self-service MVP specifications

- [Customer Onboarding and Free Tier](docs/11-customer-onboarding-and-free-tier.md)
- [Development Gap Register](docs/12-development-gap-register.md)
- [Onboarding Acceptance Test Plan](docs/13-onboarding-acceptance-test-plan.md)
- [Free-Tier Cost Model](docs/14-free-tier-cost-model.md)
- [Product Metrics and Events](docs/15-product-metrics-and-events.md)
- [Production Google OAuth Readiness](docs/16-production-google-oauth-readiness.md)

These are development specifications, not proof that features are implemented. Verify the actual application repository and deployed commit before making implementation claims.

## Working templates

- [Customer Brief](templates/customer-brief.md)
- [Delivery Manifest](templates/delivery-manifest.md)
- [Short-Form Video Script Prompt](prompts/short-video-script.md)
- [Product Story Pack Prompt](prompts/product-story-pack.md)
- [Market Validation Research Plan](research/market-validation-plan.md)

## Current implementation boundary

This repository currently contains documentation and templates. It does not yet contain a verified deployed application, live Genspark API bridge, payment integration, or production database. Build and verify those in separate milestones.
