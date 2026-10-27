# 10 — Operations and QA Playbook

## Customer intake checklist

- [ ] Contact method works.
- [ ] Product/service and audience are understood.
- [ ] Objective and platform are clear.
- [ ] Required facts are supported by customer-provided evidence or reliable sources.
- [ ] CTA and destination are known.
- [ ] Reference assets have a rights/permission basis.
- [ ] Deadline is feasible.
- [ ] Deliverables, exclusions, revisions, price, and timeline are written.
- [ ] Customer has approved scope and terms.

## Production checklist

- [ ] Approved brief version is recorded.
- [ ] Prompt template and version are recorded.
- [ ] Tool used is recorded accurately.
- [ ] Unsupported claims are removed or flagged.
- [ ] Customer-specific data is handled according to the agreed scope.
- [ ] Outputs are saved with project ID and version.
- [ ] QC is complete.
- [ ] Owner approval is explicit.

## Quality control rubric

Score each item 0–2:
1. Brief alignment.
2. Factual support.
3. Audience relevance.
4. Clarity.
5. Specificity and originality.
6. Brand voice.
7. Platform fit.
8. CTA clarity.
9. Rights, privacy, and safety.
10. Formatting and file integrity.

Proposed release threshold: 17/20 and no zero for factual support, brief alignment, or rights/safety. Hold the work if any critical issue remains, regardless of total score.

## Delivery checklist

- [ ] All promised files included.
- [ ] Filenames are clear and versioned.
- [ ] File opens and matches the stated format.
- [ ] Manifest identifies each deliverable.
- [ ] Assumptions and placeholders are disclosed.
- [ ] Usage notes included if needed.
- [ ] Revision limit and deadline restated.
- [ ] Delivery recorded.
- [ ] Customer feedback requested without pressure.

## Revision policy template

Before selling, define:
- Included revision rounds.
- What counts as a revision versus a new scope.
- Time window for requesting changes.
- How factual corrections are handled.
- How new customer inputs affect timeline and price.

Do not publish this as a binding policy until the owner has reviewed and approved the exact terms.

## Research log format

| Field | Meaning |
|---|---|
| Question | What decision needs evidence? |
| Source | URL and source owner |
| Access date | Date checked |
| Observation | What the source actually says |
| Evidence class | Fact / observation / inference / hypothesis / unknown |
| Limitation | What the source cannot establish |
| Decision | What action the evidence supports |

## Incident response

1. Stop the affected workflow.
2. Protect customer access and preserve only necessary evidence.
3. Determine whether private data, a secret, a wrong deliverable, or an unauthorized action is involved.
4. Revoke exposed credentials through the provider if needed; never paste the secret into a report.
5. Notify the owner and, where appropriate, affected customers according to applicable obligations.
6. Correct the issue and document the root cause.
7. Add a prevention check and verify it.

## Release checklist

- [ ] Build succeeds.
- [ ] Tests actually run and results are recorded.
- [ ] No secrets are committed.
- [ ] Input validation and spam controls are tested.
- [ ] Access control is verified for private data.
- [ ] Mobile and desktop layouts are checked.
- [ ] Error and empty states are checked.
- [ ] Domain and HTTPS are verified.
- [ ] Backup/export is tested if persistent data exists.
- [ ] Production claims reflect observed evidence.
