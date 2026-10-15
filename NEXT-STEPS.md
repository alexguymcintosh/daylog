# NEXT-STEPS

Rewritten at every `harness-close`. Assume the next session knows nothing that is not written here. Read this after `docs/memory/MEMORY.md` and `docs/ARCHITECTURE.md`. Plans in `docs/plans/` are dated snapshots of intent; this file is the current state. If they disagree, this file is right.

## What is true now (measured 2026-10-15)

- The harness is in: kit ff410a8, skills pinned in `skills-lock.json`, hooks armed (`git config core.hooksPath` prints `.githooks`).
- `main` requires the `gates` check (`gh api repos/alexguymcintosh/daylog/branches/main/protection`).
- No product code yet; `SPEC.md` is the spec. `./test` passes an empty suite.

## Step 0: re-verify before acting on anything above

1. `python scripts/harness_lint.py`
2. `git status --short && git log --oneline -3`
3. `python scripts/harness_lint.py --doctor`

## Open threads

- Bootstrap step 9 (prove the loop): run it as the first feature. `harness-plan feature timeline` from SPEC.md v1 piece 1, then `harness-close`; after CI is green with a coverage report, `python scripts/harness_lint.py --ratchet --update-baseline`.
- Bootstrap step 7: run `bmad-project-context` with intent adopt once code exists.

## Traps, in the order they will bite

1. `harness-close` copies the raw transcript into this public repository. A session that discusses anything private publishes it. Keep sessions here to the code, or the owner rules on private repositories first.
2. `main` is protected: work on a branch and open a pull request; merge when `gates` is green.
3. Hooks need the executable bit; if a fresh clone ignores them, run `chmod +x .githooks/*`.

## Kickoff text (paste into the next session)

> Read NEXT-STEPS.md in full, then AGENTS.md, then docs/memory/MEMORY.md, then docs/ARCHITECTURE.md. Run harness-open. Then: harness-plan feature timeline from SPEC.md v1 piece 1.
