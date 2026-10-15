# Architecture map

last_reviewed: 2026-10-15

The one living map of this repository: components, flows, boundaries and invariants. Read it before touching unfamiliar code; update it in the same change that moves structure (`harness-close` step 3). It describes this repository only. Each invariant cites the defect or decision that bought it. Factual claims carry a `verify:` line so the lint fails on the commit that makes them false.

## What this repository is

daylog lines up the activity streams one person already captures into one row per minute, and asks them on their phone about every gap. It is for an owner who wants a complete, labelled record of their own day without a model reading it.

## Layout

| Path | Holds | Owner doc or skill |
|---|---|---|
| `SPEC.md` | the product spec: v1 is timeline, blanks, ask, answer | `SPEC.md` |
| `scripts/` | harness lint, transcript copier, push check | `AGENTS.md` section 6 |
| `.agents/skills/` | harness, BMAD, ponytail, caveman and grill-me skills | `AGENTS.md` section 2 |
| `docs/` | this map, ADRs, memory, plans, session records | `AGENTS.md` section 3 |

## Flows

1. None built yet. Planned (`SPEC.md`): spool -> one row per minute -> blanks of 15+ minutes -> one phone push per blank -> the answer back into the spool.

## Boundaries and invariants

- **Data stays out of the repository.** Spool rows, timelines and answers are ignored by git. Bought by: the owner's rule, code public and data private (`SPEC.md`).
  <!-- verify: present '\*\.jsonl' in .gitignore -->
  <!-- verify: exists AGENTS.md -->
  <!-- verify: exists docs/adr/README.md -->
  <!-- verify: exists docs/memory/MEMORY.md -->
  <!-- verify: exists docs/sessions/README.md -->
  <!-- verify: exists scripts/harness_lint.py -->
  <!-- verify: exists scripts/save_transcript.py -->
  <!-- verify: exists .githooks/pre-commit -->
  <!-- verify: exists .githooks/pre-push -->
  <!-- verify: exists .github/workflows/harness-gates.yml -->

## Deliberately not built yet

- The local model that writes an evening reflection: add when v1 has run a full logged day (`SPEC.md`, layer 2).
- Phone-side capture (screen time, voice answers): add when the phone is the owner's only phone.
