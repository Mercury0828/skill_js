# CLAUDE.md — {{PROJECT_NAME}}
<!-- Copy to the project root as CLAUDE.md and fill every {{...}}. Claude Code reads this file automatically at session start — it is the entry point to everything else. -->

## Project identity
- Project: {{PROJECT_NAME}} ({{ONE_LINE_PITCH}})
- Owner: Jason (Jiachen Shen). Executor codename: {{AGENT_CODENAME}}.
- Target venue/deadline: {{VENUE_AND_DATES}}
- GitHub remote: {{REPO_URL}} — push after every milestone/phase. [rule]

## Session-start protocol (do this before any work) [rule]
1. Read `guide.md` (the constitution — it wins over any other instruction in case of conflict).
2. Read `PROJECT_STATE.md` (current phase, exact next action, open questions).
3. Read the last phase report in `docs/` if one exists; run `git log --oneline -10` and reconcile with the state file (if they disagree, trust files+git and log a correction).
4. State the resumed task in one line, then work.

## Operating rules (standing) [rule]
- Do not stop mid-run to ask the owner questions. When blocked: log to PROJECT_STATE.md open_questions with a documented assumption, proceed, flag in the phase report.
- Update PROJECT_STATE.md after every major step (artifact-based resume: any fresh session must resume from files alone).
- Self-audit against the phase's acceptance criteria (in guide.md) before declaring a phase done; never silently skip an acceptance item.
- Escalations (novelty hits, structural surprises, downgrade triggers, contradicted killer figures) go in the phase report + open_questions — finish the phase first.
- Granular commits; every phase ends with `docs/phaseN_report.md` + git tag `phaseN-done` + push.
- Verbatim quotes from papers: ≤15 words each, always with a section pointer.
- Stochastic checks: a single PASS ≠ verified — repeat 5–10×, report the stable rate.
- Independent reviews: one-shot clean-context subagents returning one decisive recommendation; no resumable review threads.
- For style edits to paper prose: propose-then-approve, one by one; never auto-apply rewrites.

## Conventions
- Figures reproducible from `experiments/<name>/config.yaml + run.py`; no notebook-only results; seeds fixed and logged. [default: ≥20 seeds, mean ± 95% CI]
- Results dir git-ignored except summary csv/png; PDFs and binaries forced binary via .gitattributes.
- arXiv PDFs may carry encryption flags — extract text with `pdftotext`, don't trust PDF readers.
- Build/toolchain pin: {{TOOLCHAIN_AND_BUILD_COMMAND_IF_LATEX}}

## File map
- `guide.md` — constitution (owner-authored; agent flags discrepancies, never silently rewrites)
- `PROJECT_STATE.md` — live state | `DESIGN_DECISIONS.md` — numbered decision log
- `docs/` — papers/, dossiers, verdicts, phase reports, writing assets
- {{SOURCE_LAYOUT_PER_GUIDE}}
- Skill reference (read on demand, not auto): https://github.com/Mercury0828/skill_js
