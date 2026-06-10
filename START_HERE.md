# START_HERE — Launching a new research project

## What you (Jason) prepare

1. **The idea, pressure-tested.** Before any code or agent time: a one-paragraph pitch, the gap statement, and the 2–4 closest competitors you already know. If you can't state what every neighbor does NOT do, the idea isn't ready for a guide.
2. **`guide.md`** — the project constitution, per `skills/02_guide_authoring.md`. Write it yourself or co-write with a supervisor chat model, then freeze it. Quality bar: a fresh agent reading only this file should be able to run the project for weeks.
3. **A GitHub repo** (can be empty or with a bare README) for milestone syncing.
4. **Your supervision schedule.** Decide which gates require your acknowledgment (typically: phase-0 novelty escalations, structural model changes, downgrade triggers, paper-story changes). Everything else the agent decides and logs.

## Repo seeding (5 minutes)

```
new-project/
├── guide.md                 # your constitution
├── CLAUDE.md                # from templates/CLAUDE_TEMPLATE.md, placeholders filled
├── .gitignore               # from templates/gitignore.template
├── .gitattributes           # from templates/gitattributes.template
```
`git init`, commit, wire the remote, push. Done.

## The kickoff prompt

Instantiate `templates/kickoff_prompt.template.md`. Its anatomy (keep all six parts):
1. **Identity & roles** — agent codename, owner, the constitution's authority ("if this prompt conflicts with guide.md, guide.md wins").
2. **Step 0** — read `guide.md` IN FULL before anything else. Non-negotiable.
3. **Session goal** — explicitly bounded (e.g., "bootstrap + Phase 0; nothing beyond").
4. **Task list** — bootstrap steps, then the phase's task list (point to guide.md as authoritative; summarize, don't fork).
5. **Acceptance criteria** — copied from the guide's phase plan; instruct self-audit against them before declaring done.
6. **Operating rules** — the standing set (no mid-run questions; artifact-based resume; escalate-in-report; granular commits; milestone push).

## What the agent will do (so you can verify)

- Bootstrap: skeleton dirs, `PROJECT_STATE.md` + `DESIGN_DECISIONS.md` seeded from the guide's appendices, doc stubs, first commit, remote push.
- Phase 0 (literature & novelty) per `skills/04_literature_and_novelty.md`: parallel paper acquisition + model-level extraction, delta verdicts with primary-source quotes, parameter-calibration table, Table-1 draft, phase report, tag `phase0-done`, push.
- Every later session: resume from `CLAUDE.md` → `PROJECT_STATE.md` → `guide.md`, execute the next phase, self-audit, report, tag, push.

## Your review points per phase

Read, in order: `docs/phaseN_report.md` (deviations + escalations + GO/STOP input), then `PROJECT_STATE.md` open_questions. Answer the OQs addressed to you; the agent proceeds on documented assumptions for the rest.
