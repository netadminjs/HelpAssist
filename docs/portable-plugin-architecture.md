# Portable Plugin Architecture Strategy

## Why This Changes the Approach

If this solution is intended to be shared with other districts, architecture should separate:
- Core intake workflow logic (stable).
- District-specific integrations (variable).

This reduces rewrites when changing phone systems, ticket systems, identity sources, and policy rules.

## Recommended Architecture Model

## Core Platform

Owns:
- Intake session orchestration.
- Question flow/state machine.
- Validation and normalization.
- Audit logging and retention jobs.
- Rules engine for schedule-aware messaging.

Does not directly depend on:
- Mitel specifics.
- 1to1plus specifics.
- Any single speech or telephony vendor.

## Plugin Interfaces

1. Telephony adapter (`ITelephonyAdapter`)
- Responsibilities:
  - Receive call events.
  - Play prompts / collect DTMF / capture recordings.
  - Return normalized caller/session data.
- Initial plugins:
  - `asterisk-agi`
  - future `mitel-native` (if needed)

2. Ticket delivery adapter (`ITicketDeliveryAdapter`)
- Responsibilities:
  - Submit normalized intake as ticket.
  - Return external ticket reference and status.
- Initial plugins:
  - `email-to-ticket` (for 1to1plus)
  - future API-based adapters (Freshservice, Zendesk, etc.)

3. Speech adapter (`ISpeechAdapter`)
- Responsibilities:
  - STT transcription.
  - Confidence scoring.
- Initial plugins:
  - `none` (DTMF-first MVP)
  - future offline `whisper.cpp` or similar.

4. Directory/identity adapter (`IIdentityAdapter`) (future)
- Responsibilities:
  - Optional caller identity verification or enrichment.
- Phase-1 default:
  - `trust-model` plugin.

## Configuration Model

Use layered config to avoid hardcoding district assumptions:
- Global defaults.
- District profile (sites, aliases, support hours, holidays).
- Environment secrets and network endpoints.

Example district profile content:
- Site alias table.
- Site-to-sender mappings.
- Business hours and closure dates.
- Prompt language and wording overrides.

## Repo and Version-Control Strategy

Use Git and GitHub from day one:
- Keep full architecture history and decision trail.
- Enable controlled collaboration and reuse by other districts.

Recommended baseline:
- Main branch protection.
- Pull-request workflow.
- Semantic versioning tags (`v0.1.0`, `v0.2.0`, ...).
- Changelog for district admins.
- `CONTRIBUTING.md` and issue templates.

## Packaging and Reuse

Create a reference deployment package with:
- Core service container image.
- Plugin packages (telephony, ticket delivery, speech).
- Sample district config (`district.example.yaml`).
- Minimal deployment guide.

This allows another district to:
1. Pick telephony plugin.
2. Pick ticket adapter.
3. Fill district config.
4. Deploy without source edits.

## Security and Governance for Open Sharing

- Never commit real district credentials, IP inventories, or personally identifying test data.
- Provide `.env.example` and config templates only.
- Include a clear license (for example MIT or Apache-2.0) after district approval.
- Document data handling boundaries (recordings/transcripts/retention).

## Practical Recommendation for This Project

1. Build phase 1 for Maryville with adapter boundaries in place.
2. Keep first implementation simple (`asterisk-agi` + `email-to-ticket`).
3. Avoid over-engineering until pilot proves call flow and ticket quality.
4. After pilot stability, extract reusable plugin SDK/docs and publish repository.

This keeps delivery speed high while preserving portability.
