# Research Startup Package (skill_js)

Jason's reusable kit for launching AI-assisted research projects from zero. Drop a project constitution (`guide.md`) into a fresh repo, follow `START_HERE.md`, and Claude Code bootstraps and runs the project under these protocols.

Provenance: distilled from two completed/running projects — CDRO (IEEE TSG paper, full revision cycle) and PROSE (INFOCOM 2028, autonomous phase execution). Everything here is domain-agnostic; project-specific content never belongs in this repo.

## How to launch a new project (3 steps)

1. **Author the constitution.** Write (or have a supervisor model write) `guide.md` for the new idea, following `skills/02_guide_authoring.md`. This is the highest-leverage hour you will spend.
2. **Seed the repo.** New directory + `git init` + GitHub remote. Copy in: `templates/CLAUDE_TEMPLATE.md` → `CLAUDE.md` (fill the placeholders), `templates/gitignore.template` → `.gitignore`, `templates/gitattributes.template` → `.gitattributes`. Put `guide.md` at the root.
3. **Fire the kickoff prompt.** Instantiate `templates/kickoff_prompt.template.md` (fill project name, phase-0 scope, repo URL) and paste it into Claude Code launched at the repo root. The agent bootstraps the skeleton, seeds the state files, and executes Phase 0.

After that, each new session resumes from `CLAUDE.md` + `PROJECT_STATE.md` + `guide.md` alone — no conversation memory required.

## Contents

| Path | What it is |
|---|---|
| `START_HERE.md` | The launch protocol in detail (owner-side checklist + what the agent will do) |
| `skills/01_project_memory.md` | Three-layer memory, resume protocol, git/sync discipline, division of labor |
| `skills/02_guide_authoring.md` | How to write a `guide.md` constitution — structure + quality bar |
| `skills/03_phase_discipline.md` | Phases, acceptance criteria, self-audit, escalation, downgrade triggers |
| `skills/04_literature_and_novelty.md` | Phase-0 playbook: parallel extraction, delta verdicts, quote discipline, parameter calibration |
| `skills/05_theory_verification.md` | Re-derivation, symbolic+numerical cross-checks, traps and fallbacks |
| `skills/06_experiment_discipline.md` | Configs/seeds/unit-tests-vs-theory, figure & table integrity |
| `skills/07_writing_and_style.md` | Writing rules + the anti-AI-flavor system (checklist is a copyable template) |
| `skills/08_review_and_submission.md` | Multi-reviewer simulation, frozen concern table, LaTeX/page mechanics |
| `skills/09_tooling_gotchas.md` | Hard-won practical notes (Windows, git, PDFs, paywalls) |
| `templates/` | Copy-in artifacts: CLAUDE.md, kickoff prompt, state files, phase report, novelty verdict, writing assets, AI style checklist, git config |
| `RESEARCH_PROTOCOL.md` | Jason's standing directives stream (canonical copy) |

## Maintenance rules

- This repo is the **canonical home** of the skill set. Project repos may carry a local `SKILL.md` pointer + project-specific lessons; generalizable lessons migrate HERE at phase boundaries.
- Every entry must be domain-agnostic and earned (from a real project incident or decision) — no speculative best practices.
- Defaults marked `[default]` are tunable per project; rules marked `[rule]` are not.
