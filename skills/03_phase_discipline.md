# Skill 03 — Phase discipline, self-audit, escalation

## Phase mechanics [rule]
- Ordinal phases (not calendar-locked); each phase's acceptance criteria are written in the guide BEFORE the work starts.
- Acceptance = trend-matching unless a constant is explicitly pinned.
- Every phase ends with: self-audit table (criterion → PASS/FAIL/NOT-DONE-because) → `docs/phaseN_report.md` → git tag `phaseN-done` → push.
- Never silently skip an acceptance item; log NOT-DONE with reasons instead.
- A surprising result (metric ordering violated, figure shape contradicted) is a bug OR a finding — classify with evidence before proceeding; silent shape-forcing is forbidden.

## Phase report contents (template in templates/phase_report.template.md)
What was done → evidence highlights (what changed the project's picture) → deviations from the guide (each logged where it lives) → NOT-OBTAINED/NOT-DONE log with trails → open questions & escalations (mirrored in PROJECT_STATE) → self-audit table → GO/STOP input for the next phase, with bindings ("GO, provided X is worded as Y").

## Escalation protocol [rule]
Escalate-in-report, not halt-in-run. Triggers (typical set — instantiate per guide):
- Novelty verdict YES or strong-PARTIAL in literature checks (mark `ESCALATION REQUIRED` atop the verdict file AND in open_questions; still finish the phase).
- Any structural model change; downgrade-trigger activation; killer-figure shape contradiction; anything that changes the paper's story.
A strong-PARTIAL on a *sub-axis* (not the core gap) is still an escalation: it usually forces re-scoped novelty wording and tighter citation discipline, and that binding must be recorded as a constraint on the next phase.

## Downgrade triggers
Risky/bonus tracks get a pre-committed trigger in the guide ("N focused weeks, then fallback"). When the moment comes, the decision is cheap because it was already made. Document counterexamples found — they may themselves be content.

## Showable-artifact milestone
At a pre-agreed midpoint: tag + bundle `src + experiments + tests + configs + DESIGN_DECISIONS.md + smoke results` (exclude data/artifacts) + a WALKTHROUGH.md for one focus component (math + code refs + numerical sanity table + vs-degenerate comparison). Do not let this stall later phases.

## Verification habits that gate "done"
- Stochastic checks: repeat 5–10×, report the stable rate; one PASS is not verified. [rule]
- Independent review = one-shot clean-context subagent with the question + all artifacts + "return one complete, decisive recommendation"; no resumable review threads. [rule]
- Before any state-changing/destructive operation on artifacts you didn't create: look first; if reality contradicts the description, surface it instead of proceeding.

## Verification tooling as committed scripts, not shell history (EAGER Phase 1B)
Commit the phase-gate protocol as two one-command scripts at Phase 0/1, then
reuse them at EVERY later gate:
- **Repeat runner** (`scripts/run_repeat_suite.py`): N subprocess pytest runs
  of the flaky-prone marker (`-m stochastic`), junitxml into a TEMP dir (test
  hygiene), aggregated into a per-test pass-count table, non-zero exit unless
  every test is N/N. The table is the PHASE_STATUS evidence artifact.
- **Clean-state verifier** (`scripts/clean_state_verify.py`): fresh `git
  clone` + fresh venv + install, run the end-to-end artifact script BEFORE
  the test suite, run pytest, run the script again; require byte-identical
  script output and an unchanged file-tree snapshot (diff excluding
  interpreter/runner caches: __pycache__, .pytest_cache, *.egg-info). The
  tree diff catches test pollution that `git status` misses because ignored
  paths (results/) don't show there.
Rationale: the per-phase protocol (fresh checkout, 10× repeats, no-pollution
sandwich) degrades into unreproducible shell history unless it is code; a
verifier that exits non-zero also composes into CI later. [rule]
