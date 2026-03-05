# Repository Structure

## Directories

- `core/`: orchestration, contracts, validation, scheduling, retention jobs.
- `plugins/telephony/`: PBX/voice intake adapters.
- `plugins/ticket/`: ticket delivery adapters (email/API).
- `plugins/speech/`: optional STT adapters.
- `districts/`: district config profiles and examples.
- `docs/`: public architecture and operations docs.

## Private vs Public

- Public-safe: architecture, interfaces, examples, templates.
- Private: district inventories, internal IPs, staffing notes, pilot logs.

Store private content in `internal/` (ignored by git).
