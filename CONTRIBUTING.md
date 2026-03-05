# Contributing

## Workflow

1. Create a feature branch.
2. Make small, focused changes.
3. Open a pull request with:
- summary of change,
- risk notes,
- test/validation notes.

## Standards

- Keep district-specific data in config, not core code.
- Keep adapters behind stable interfaces.
- Do not commit secrets or private operational details.

## Commit Style

Use clear, scoped commit messages, for example:
- `core: add intake session model`
- `plugin/email: add smtp sender mapping`
- `docs: update adapter contract examples`
