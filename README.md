# AI Voice Helpdesk Intake

Reusable, plugin-based intake platform for K-12 IT helpdesks.

## What This Repo Is

This repository is the **public/shareable scaffold** for a phone-first intake workflow that can:
- collect issue details from callers,
- normalize request data,
- send to a ticketing destination (email/API adapter),
- support district-specific configuration without changing core code.

## Architecture Direction

- Core workflow engine in `core/`
- Replaceable adapters in `plugins/`
- District configuration profiles in `districts/`

See [portable-plugin-architecture.md](/Users/james.saniger/Library/CloudStorage/OneDrive-MaryvilleCitySchools/projects/aivoicehelpdesk/docs/portable-plugin-architecture.md).

## Repository Layout

- `core/` core intake orchestration and domain contracts
- `plugins/` telephony/ticket/speech adapters
- `districts/example/` safe sample district config
- `docs/` public docs and implementation guidance
- `internal/` private district notes (git-ignored)

## Quick Start (Scaffold Stage)

1. Copy `districts/example/district.example.yaml` to your district config file.
2. Implement or select adapters in `plugins/`.
3. Wire config values for your PBX and ticketing destination.
4. Add runtime secrets via environment variables (not committed).

## Privacy and Security

Do not commit:
- real IP addresses,
- credentials,
- staff/student PII,
- production call recordings/transcripts.

## Current Status

Scaffold and architecture docs only. Implementation tasks are tracked in private district planning docs.
