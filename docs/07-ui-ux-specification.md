# 07 — UI/UX Specification

## Design direction

Premium, clean, modern, elegant, and calm. Embrilo should feel like a reliable creative partner, not a generic AI tool dashboard. Prefer strong typography, generous spacing, restrained colors, clear hierarchy, and real examples with honest labels.

## Public information architecture

- Home
- Services / packages
- How it works
- Examples (clearly marked as concept samples until real client work exists)
- FAQ / terms
- Start a brief
- Contact

Do not create empty pages simply to make the sitemap look complete.

## Landing page structure

1. **Hero:** one clear statement of the outcome; one primary CTA.
2. **What Embrilo delivers:** exact outputs and formats.
3. **Who it is for:** one initial target segment after validation.
4. **How it works:** brief → scope → production → human QC → delivery.
5. **Sample work:** concept-labelled examples with a short explanation.
6. **Package / pricing:** publish only after scope and economics are checked; otherwise explain how to request a quote.
7. **Quality promise:** describe the actual review process, not unsupported performance guarantees.
8. **FAQ:** turnaround, revisions, rights, AI assistance, customer inputs, privacy.
9. **Final CTA:** start a brief or contact Embrilo.

## Brief form fields

Required: name or business identifier, contact method, product/service, target audience, objective, platform, desired format, main message, CTA, deadline range, and rights confirmation for supplied materials.

Optional: brand voice, prohibited terms, examples, existing copy, and notes.

Form behavior:
- Clear labels and examples.
- Explain why a field is needed.
- Validate on client and server.
- Preserve non-sensitive input after recoverable errors where practical.
- Do not require file upload if a link or description is enough.
- Show a clear success state only after the server confirms receipt.
- Provide an alternate contact method if submission fails.

## Internal operator view (later MVP)

- Queue by status and due date.
- Brief details and missing-information checklist.
- Scope / quote.
- Payment verification state.
- Production run and prompt version.
- QC checklist and reviewer.
- Deliverable manifest and revision history.
- Time and cost log.
- Audit trail.

Keep the operator area private. Do not rely on a hidden URL as authentication.

## Design tokens (initial hypotheses)

- Background: warm off-white or near-white.
- Primary text: deep charcoal.
- Secondary text: muted neutral.
- Accent: one restrained, distinctive brand accent; final palette to be chosen after visual prototypes.
- Typography: one legible sans-serif family, with optional display treatment used sparingly.
- Radius: modest; avoid excessive pill-shaped cards.
- Shadows: subtle and used only to establish hierarchy.
- Motion: minimal, reduced-motion friendly.

These are design directions, not a finalized logo or approved palette.

## Accessibility

- Keyboard navigation for all controls.
- Visible focus indicators.
- Sufficient color contrast.
- Form errors associated with fields.
- Semantic headings and buttons.
- Alt text for meaningful images.
- Avoid relying on color alone.
- Respect reduced-motion preferences.
- Test at mobile widths and zoom.

## Content tone

Use direct, warm, confident Indonesian. Avoid inflated terms such as “revolutionary,” “guaranteed viral,” or “fully autonomous” unless a precise, supportable claim exists.


## Self-service journey addendum (2026-10-29)

Add a distinct path: landing CTA “Coba gratis” → short onboarding with defaults/optional skips → Google sign-in → workspace with server-derived allowance → supported generator → progress/status → private result/download → history and honest next steps. Do not require a service brief for self-service users. Design OAuth cancellation, expired session, quota unavailable, loading, empty, provider failure and network failure states. Keep paid checkout inactive until verified. See docs/11-customer-onboarding-and-free-tier.md.


## Self-service journey addendum (2026-10-29)

Add a distinct path: landing CTA “Coba gratis” → short onboarding with defaults/optional skips → Google sign-in → workspace with server-derived allowance → supported generator → progress/status → private result/download → history and honest next steps. Do not require a service brief for self-service users. Design OAuth cancellation, expired session, quota unavailable, loading, empty, provider failure and network failure states. Keep paid checkout inactive until verified. See docs/11-customer-onboarding-and-free-tier.md.
