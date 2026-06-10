# Skill 01 — Project memory, continuity, and division of labor

The single most load-bearing habit: a fresh agent session (or the human after a week away) must resume in ~5 minutes **from files alone**. No conversation memory is ever assumed.

## Three-layer memory [rule]

| Layer | File | Discipline |
|---|---|---|
| Constitution | `guide.md` (+ `CLAUDE.md` as the auto-read entry point) | Durable: identity, locked decisions, phase plan with acceptance criteria, ground rules. Owner-authored; the agent flags discrepancies, never silently rewrites owner config. |
| Live state | `PROJECT_STATE.md` | Overwritten after every major step: current phase, last artifact, **exact next action**, open questions with owner-addressed flags, deviations log, operational notes. Blind-resumable. |
| Audit trail | phase reports + granular commits (+ per-task change logs in writing-heavy phases) | Append-only. One log per atomic task with before→after evidence and build/test status. Never squash or edit old entries. |

Key insight from practice: Claude Code auto-reads `CLAUDE.md`, NOT `guide.md` — so `CLAUDE.md` must contain the session-start protocol that chains into everything else.

## Session-start protocol [rule]
1. `CLAUDE.md` → `guide.md` → `PROJECT_STATE.md` → last phase report / change log.
2. `git status` + `git log --oneline -10`; if state file and git disagree, trust files+git, append a correction note.
3. Say the resumed task in one line. Then work.

## Decision log
`DESIGN_DECISIONS.md`: numbered (D0, D1, …), dated, with rationale and dependencies. Locked decisions are not reopened without owner escalation. Forced deviations get a new numbered entry, never an edit of the old one.

## Git & sync [rule]
- Wire the GitHub remote on day 0; push after every milestone/phase. If the remote has an initial commit, merge with `--allow-unrelated-histories` rather than force-pushing.
- `.gitattributes` forces `*.pdf` and data binaries to binary (a PDF treated as text gets CRLF-corrupted on Windows checkout — observed in practice).
- Track figure-generating code the moment it exists; untracked generators are a recovery hazard.
- New machine: reconcile state files vs git before touching anything; flag stale paths in owner-owned config, don't rewrite them.

## Division of labor
- **Agent:** proposes, executes, verifies, bookkeeps; detects contradictions (physics, table↔figure, novelty) and flags them; decides everything not gated.
- **Owner:** authors/owns the constitution and config; answers gated decisions (novelty escalations, structural changes, downgrade triggers, story changes, style-edit approvals); supplies external inputs (reviewer feedback, paywalled papers, venue decisions).
- Owner-issued standing rules get recorded with date + scope (e.g., "flag only, never re-audit") so later sessions don't relitigate them.
- No mid-run questions to the owner [rule]: blocked → documented assumption in open_questions → proceed → flag in phase report.
