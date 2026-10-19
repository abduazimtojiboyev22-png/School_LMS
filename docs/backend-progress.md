# Backend prompt progress

Updated: 2026-10-19  
Rule: complete one prompt at a time, in sequence. P000 is the governing prompt and is not part of the 98 implementation prompts.

## Status meanings

- `not_started`: no implementation work has been done for this prompt.
- `in_progress`: the current prompt is being implemented; do not start another prompt.
- `implemented_unverified`: changes exist, but acceptance checks have not all passed.
- `verified`: implementation and its stated acceptance checks have evidence recorded below.
- `blocked`: a required dependency or external condition prevents completion; record the evidence and smallest blocker.

Do not mark a prompt `verified` based only on code being present. Do not reset databases or delete migrations to make a prompt pass.

## Current state

- P000: applied as the governing instructions; no implementation change.
- Current prompt: P001 — `verified` (documentation-only acceptance checked).
- Next prompt: P002 — `not_started`.
- No later prompt has been started.

## Prompt ledger

| Prompt(s) | Initial status |
|---|---|
| P001 | `verified` |
| P002–P023 | `not_started` |
| P023-A, P023-B, P023-C, P023-D, P023-E, P023-F | `not_started` |
| P024–P080 | `not_started` |
| P081 | `not_started` |
| P081-A, P081-B | `not_started` |
| P082–P090 | `not_started` |

For each prompt, record its status, changed files, checks actually run and their results, blockers, and the next prompt. Split ranges into individual rows as work progresses; never imply that an entire range is complete because one prompt passed.

## P001 evidence

- Added `docs/backend-scope.md` with the one-school, pupil/teacher, backend-only boundary, repository facts, technology direction, and the P002 prerequisite.
- Added this progress ledger and recorded P001 as verified only after checking the written acceptance criteria.
- Acceptance: documentation only; no app, model, migration, API endpoint, or dependency was added.
- Verification performed: inspected the repository tree, `root/settings.py`, `requirements.txt`, `.env.example`, `.gitignore`, and migration directory; read back both new documents for scope and sequence consistency. No automated test was required for this documentation-only prompt.
- Known limitation: the architecture PDF was unavailable, so PDF alignment remains unverified.
