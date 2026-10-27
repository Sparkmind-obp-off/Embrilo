# 04 — Product Requirements Document (PRD)

## Product goal

Enable a customer to understand Embrilo's offer, submit a usable brief, receive a clear scope, and let the owner manage delivery reliably. Keep manual operations acceptable for the first version.

## Users

- **Prospective customer:** evaluates the offer and starts an inquiry.
- **Customer:** submits project details and receives deliverables.
- **Operator / founder:** validates briefs, prepares quotes, manages production, QC, and delivery.
- **Reviewer:** initially the founder; may be a separate role later.

## MVP user journeys

### Customer
1. Visit landing page.
2. Understand deliverables, process, limitations, and next step.
3. Submit brief or contact request.
4. Receive acknowledgement (manual until tested automation exists).
5. Approve written scope and payment instructions.
6. Receive delivery and revision guidance.

### Operator
1. Review incoming brief.
2. Mark complete, clarification needed, or declined.
3. Define scope and quote.
4. Record payment status based on verified evidence.
5. Produce and review outputs.
6. Deliver files and record completion.
7. Log feedback, time, cost, and lessons.

## Must-have requirements

- **FR-001:** Public page accurately describes the current service.
- **FR-002:** Service offer states exact outputs, exclusions, revision limit, and expected timeline.
- **FR-003:** Brief intake captures required business, audience, objective, platform, tone, CTA, references, deadline, and contact fields.
- **FR-004:** Inputs are validated and missing required information is flagged.
- **FR-005:** Customer references include a rights/permission confirmation.
- **FR-006:** Operator can track status: new, needs clarification, qualified, quoted, awaiting payment, paid/approved, in production, QC, revision, delivered, cancelled.
- **FR-007:** Quote and agreed scope can be recorded.
- **FR-008:** Payment is not marked confirmed without verified evidence from the configured method.
- **FR-009:** Deliverables pass the human QC checklist before release.
- **FR-010:** Final package has a manifest and version identifier.
- **FR-011:** Customer can understand the revision process.
- **FR-012:** Owner can export or back up essential project records.
- **FR-013:** Errors and blocked integrations are visible to the operator.

## Non-functional requirements

- Mobile-first, responsive, accessible form labels and keyboard navigation.
- Indonesian copy by default.
- No secrets in client code, logs, or Git.
- Minimize personal data collection and restrict access to customer files.
- Server-side validation for all trusted decisions.
- Safe file upload constraints if uploads are implemented.
- Avoid storing sensitive content longer than necessary.
- Graceful handling of network and integration failures.
- Basic observability without exposing brief contents unnecessarily.

## MVP exclusions

- Full multi-tenant SaaS.
- Autonomous social publishing.
- Guaranteed viral reach or conversion.
- Automated payment reconciliation without a verified provider integration.
- Complex subscriptions, coupons, and affiliate systems.
- Public customer accounts unless needed by evidence.
- Automated video rendering pipeline unless the tool access and economics are proven.
- Customer-facing AI chatbot making commitments.
- Unreviewed AI content delivery.

## Acceptance criteria

- A test customer can understand the offer and submit a valid brief.
- Invalid fields receive actionable error messages.
- An operator can move a project through the defined states.
- Scope, price, and revision terms are recorded before production.
- A project cannot be labelled delivered before QC and approval.
- A delivered package has filenames, version, and handover notes.
- A basic backup/export procedure is documented and tested.
- All claims about payment, deployment, and integrations match actual evidence.

## Product decisions

Use a public landing page plus a lightweight intake form first. If the owner can reliably manage the first projects with a private spreadsheet or structured project files, defer authentication and a database-backed dashboard. Add application complexity only when manual tracking becomes a demonstrated bottleneck.
