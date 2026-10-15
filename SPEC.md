# SPEC — daylog: data in, minute by minute

_Prepped 2026-10-15. Not fired. The first repo on Matt's kit. Spec section that covers it:
`/home/shmacka/system/AGENTS.md` › Cyber › "Day log"._

**Heard:** "the system that sends messages to my graphene to build a full day minute by minute log … priority is
data … use Matt harness, let's start with data in."
**Build:** code that lines up the streams already captured into one minute timeline, and asks him on the phone
about every blank. No model in v1.
**Pays:** every answer is a labelled row about his own day, which is the data moat ALEX.md Part II is built on.

## Step 0 — bootstrap Matt's kit
Follow `https://raw.githubusercontent.com/mattgtwk/MKC_Agentic_dev_harness/main/BOOTSTRAP.md` in this folder.
Its three questions, answered: repo `alexguymcintosh/daylog`, **public**; stack Python 3 stdlib; test command
`pytest --cov --cov-branch --cov-report=xml`. Commit this SPEC.md as the second commit. Then `harness-open`,
then `harness-plan feature daylog` built from this file, and **stop for his approval of the plan.**

## What exists (take it, do not rebuild)
- **The streams:** `~/.local/share/capture/spool/*.jsonl` on shmacka-tp: 20 streams (shell, browser, git,
  claude, place, power, input, media and others), shipped to the Pi by capture's seat shipper.
- **The phone channel:** private ntfy on `shmacka-pi` (`ntfy.service`, running). Phone side: SPEC-tonight.md.
- **The asker:** `twin-ask` in `/home/shmacka/cyber/twin/`, laptop-only, waiting on a phone channel.
- **The record contract:** rows go through `emit` into the spool, like every other stream.

## v1 — the four pieces
1. **Timeline** — every spool stream → one row per minute: which streams were active. Code, no model.
2. **Blanks** — any run of 15+ minutes with nothing active, 07:00–23:00, becomes one ask.
3. **Ask** — one ntfy push: "14:20–15:05 is blank. What were you doing?" with preset buttons
   (moving · eating · people · deep work · rest) and "other", which opens a small page on the Pi to type.
4. **Answer** — one row back through `emit`, `source=daylog`, keyed to the blank it answers.

## Invariants
- **The push text is built from timestamps only.** No stream content (browser titles, shell lines) ever
  enters a notification.
- **The ask topic is not the approval topic.** The judge's channel stays separate.
- **No model in v1.** Layer 2 is a local model on orbit (RTX 3050, 6 GB) writing the evening reflection,
  because the day is identifying data. That reverses his twin-build ruling "no local models"; his call when
  layer 2 is specced.
- **Code public, data private.** No spool row, answer or timeline is ever committed.

## Done when
- A fixture day with planted gaps produces exactly those asks and exactly those rows (`pytest`).
- Live: by 22:00 on the first full day, every 15-minute block from 07:00 to 23:00 is filled by a stream or
  answered from the phone.

## Not in scope
The local model · reflection and forecast questions · phone-side capture (screen time) · voice answers.

## Open — recommended answers, change any
- Blank size 15 min · quiet hours 23:00–07:00 · at most 1 ask per 30 min, so it never nags.
- Where it runs: the Pi, beside ntfy and the shipped store.

## How it runs
One session, **Opus** orchestrating, **Sonnet** for tasks, on **shmacka-tp** (it deploys to the Pi; the orbit
seat cannot reach the tailnet). Matt's loop: open → plan → build → close. Needs the Pixel on the tailnet first.
