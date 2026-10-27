# 06 — Database Blueprint

## Status

This is a proposed schema for a later lightweight MVP. **No database is provisioned by this document.** Start with a structured private tracker if that is sufficient.

## Design rules

- Store only information required to fulfil the service.
- Use opaque IDs; do not expose sequential IDs in public URLs.
- Store timestamps in UTC and render local time for the operator.
- Keep payment status separate from project production status.
- Keep uploaded assets private.
- Do not store card data, passwords, or API keys.
- Define retention and deletion procedures before collecting real customer records.

## Proposed entities

### clients
- `id` TEXT PRIMARY KEY
- `display_name` TEXT NOT NULL
- `contact_channel` TEXT NOT NULL
- `contact_value` TEXT NOT NULL
- `created_at` TEXT NOT NULL
- `retention_until` TEXT NULL

### briefs
- `id` TEXT PRIMARY KEY
- `client_id` TEXT NOT NULL REFERENCES clients(id)
- `version` INTEGER NOT NULL
- `business_or_product` TEXT NOT NULL
- `audience` TEXT NOT NULL
- `objective` TEXT NOT NULL
- `platform` TEXT NOT NULL
- `format_requirements` TEXT NOT NULL
- `brand_voice` TEXT NULL
- `approved_facts_json` TEXT NOT NULL
- `cta` TEXT NULL
- `references_json` TEXT NOT NULL
- `rights_confirmed` INTEGER NOT NULL DEFAULT 0
- `status` TEXT NOT NULL
- `created_at` TEXT NOT NULL

### projects
- `id` TEXT PRIMARY KEY
- `client_id` TEXT NOT NULL REFERENCES clients(id)
- `current_brief_id` TEXT NOT NULL REFERENCES briefs(id)
- `status` TEXT NOT NULL
- `scope_summary` TEXT NOT NULL
- `price_amount_minor` INTEGER NULL
- `currency` TEXT NOT NULL DEFAULT 'IDR'
- `revision_limit` INTEGER NOT NULL DEFAULT 1
- `due_at` TEXT NULL
- `created_at` TEXT NOT NULL
- `updated_at` TEXT NOT NULL

### payments
- `id` TEXT PRIMARY KEY
- `project_id` TEXT NOT NULL REFERENCES projects(id)
- `provider` TEXT NOT NULL
- `amount_minor` INTEGER NOT NULL
- `currency` TEXT NOT NULL DEFAULT 'IDR'
- `status` TEXT NOT NULL
- `provider_reference` TEXT NULL
- `verified_at` TEXT NULL
- `created_at` TEXT NOT NULL

### production_runs
- `id` TEXT PRIMARY KEY
- `project_id` TEXT NOT NULL REFERENCES projects(id)
- `brief_version` INTEGER NOT NULL
- `prompt_id` TEXT NOT NULL
- `prompt_version` TEXT NOT NULL
- `tool_name` TEXT NOT NULL
- `operator_id` TEXT NULL
- `status` TEXT NOT NULL
- `started_at` TEXT NULL
- `finished_at` TEXT NULL
- `notes_redacted` TEXT NULL

### deliverables
- `id` TEXT PRIMARY KEY
- `project_id` TEXT NOT NULL REFERENCES projects(id)
- `production_run_id` TEXT NULL REFERENCES production_runs(id)
- `filename` TEXT NOT NULL
- `media_type` TEXT NOT NULL
- `storage_key` TEXT NULL
- `version` INTEGER NOT NULL
- `qc_score` INTEGER NULL
- `qc_status` TEXT NOT NULL
- `approved_at` TEXT NULL
- `delivered_at` TEXT NULL

### audit_events
- `id` TEXT PRIMARY KEY
- `project_id` TEXT NULL REFERENCES projects(id)
- `actor_type` TEXT NOT NULL
- `event_type` TEXT NOT NULL
- `safe_metadata_json` TEXT NOT NULL
- `created_at` TEXT NOT NULL

## Status values

Project status: `new`, `needs_clarification`, `qualified`, `quoted`, `awaiting_payment`, `paid_approved`, `in_production`, `qc`, `revision`, `delivered`, `cancelled`.

Payment status: `unverified`, `pending`, `verified`, `failed`, `refunded`.

QC status: `not_reviewed`, `failed`, `changes_requested`, `passed`, `owner_approved`.

Enforce transitions in application logic. Never mark a payment verified solely because a customer says they paid.

## Indexes to consider

- `briefs(client_id, created_at)`
- `projects(client_id, status, updated_at)`
- `payments(project_id, status)`
- `production_runs(project_id, started_at)`
- `deliverables(project_id, version)`
- `audit_events(project_id, created_at)`

## Migration and backup

- Keep SQL migrations under `migrations/` with sequential names.
- Test migrations on a non-production database before applying them.
- Use synthetic seed data only.
- Document how to export and restore records.
- Verify backup integrity by restoring a test copy.
- Do not add real customer data to test fixtures or Git.
