# Skill 08 — Review simulation, revision, and submission mechanics

## Multi-reviewer simulation → frozen concern table → resolution rounds
1. **Batch of independent reviewer passes** (clean-context one-shot subagents, each with a distinct reviewer persona/focus: data integrity, physical/mathematical plausibility, overclaims, style, minor).
2. **Freeze a master concern table** — categorized (A: data/figure contradictions; B: plausibility; C: prose overclaims; D: style tokens; E: minor), each with priority and an owner-decision flag where needed. Freezing prevents goalpost drift across rounds.
3. **Single-verifier resolution rounds** against the frozen table: agent proposes fixes per concern → owner approves → serial execution → full re-audit. New issues found mid-round get appended with a flag, not silently mixed in.
4. One atomic change-log per task (files touched, before→after snippets, build status) — auditable at line level, never compressed into vague bullets.

## Revision phasing
Revise in explicit owner-approved phases (typically: experiments → model section → intro/abstract/conclusion-numbers → methodology light-touch → final terminology/claims sweep), not scattershot. Reconcile all numbers at the phase that touches them.

## LaTeX / build mechanics [rule]
- Pin the toolchain (TeX Live vs MiKTeX, version, path) in CLAUDE.md; identical source builds differently across toolchains. TeX Live doesn't auto-install packages (`tlmgr install`).
- Exact build command recorded; full multi-pass build after EVERY content change; the tracked PDF must always reflect source (a stale tracked PDF is a source-of-truth crisis on recovery).
- Every change-log records: pages, errors, undefined refs/citations, overfull/underfull counts — distinguishing pre-existing from newly introduced.
- Visual artifacts (TikZ, plots): crop-render at 300 dpi (`pdftoppm -png -r 300 …`) and inspect before declaring done; quick previews miss overlaps.

## Page-limit passes (measured, not vibes)
Locate the overflow precisely (which page, how many columns of what). Then pull levers in order of information loss:
1. Font step-downs (displays, captions, tables, algorithms);
2. Subsection merges and redundant-proposition removal;
3. Targeted prose cuts (measured per-paragraph savings);
4. Float spacing (`\vspace` negatives, `\raggedbottom`);
5. Weakest-reference deletion — respecting a venue-citation floor (e.g., keep ≥8 target-venue refs).
Each step logged with its page impact and reversible.

## Rebuttal preparation
The anticipated-rebuttal stubs (from writing_assets) + the per-attack ablation figures (from the experiment plan) mean most reviewer attacks have a pre-built answer: scoping paragraph + a figure. Maintain that mapping explicitly (attack → remark → figure).
