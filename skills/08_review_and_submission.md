# Skill 08 — Review simulation, revision, and submission mechanics

## Multi-reviewer simulation → frozen concern table → resolution rounds
1. **Batch of independent reviewer passes** (clean-context one-shot subagents, each with a distinct reviewer persona/focus: data integrity, physical/mathematical plausibility, overclaims, style, minor).
2. **Freeze a master concern table** — categorized (A: data/figure contradictions; B: plausibility; C: prose overclaims; D: style tokens; E: minor), each with priority and an owner-decision flag where needed. Freezing prevents goalpost drift across rounds.
3. **Single-verifier resolution rounds** against the frozen table: agent proposes fixes per concern → owner approves → serial execution → full re-audit. New issues found mid-round get appended with a flag, not silently mixed in.
4. One atomic change-log per task (files touched, before→after snippets, build status) — auditable at line level, never compressed into vague bullets.

## Lessons from a live five-reviewer cycle (PROSE Phase 7)
- Distinct reviewer lenses catch DISJOINT A-level issues: the data reviewer found number drift, the physics reviewer found a non-implementable primitive, the TPC reviewer found evaluation-scale gaps, the math reviewer found a surrogate-objective gap in a guarantee chain, the style reviewer found defensive framing. None overlapped. Cross-reviewer CONSENSUS items (the same flaw hit from different angles) are the highest-confidence fixes — resolve them first.
- Answer evaluation-scale and "your-method's-delta-is-invisible" concerns with NEW EXPERIMENTS, not prose; place the new experiment using the theory's regime map (a first attempt that lands in a degenerate regime wastes a run), and use PAIRED per-seed differences to resolve overlapping-CI policy comparisons (paired CI shrank a 0.25 gap from ambiguous to 17/20-seeds decisive).
- Double-rounding is a systematic error source: log prints 3 decimals → phase report quotes them → paper re-rounds. Re-derive every paper number from the generating CSVs directly (the data reviewer's mandate should say so explicitly).
- Guarantee-chain audits: when a paper claims constant γ from a cited algorithm family, verify the DEPLOYED variant's constant and the OBJECTIVE the guarantee is certified on (surrogate vs true) — the single most-flagged issue across three independent reviewers.

## Revision phasing
Revise in explicit owner-approved phases (typically: experiments → model section → intro/abstract/conclusion-numbers → methodology light-touch → final terminology/claims sweep), not scattershot. Reconcile all numbers at the phase that touches them.

## LaTeX / build mechanics [rule]
- Pin the toolchain (TeX Live vs MiKTeX, version, path) in CLAUDE.md; identical source builds differently across toolchains. TeX Live doesn't auto-install packages (`tlmgr install`).
- Exact build command recorded; full multi-pass build after EVERY content change; the tracked PDF must always reflect source (a stale tracked PDF is a source-of-truth crisis on recovery).
- Every change-log records: pages, errors, undefined refs/citations, overfull/underfull counts — distinguishing pre-existing from newly introduced.
- Visual artifacts (TikZ, plots): crop-render at 300 dpi (`pdftoppm -png -r 300 …`) and inspect before declaring done; quick previews miss overlaps.

## Post-revision fresh-reader logic pass [rule, Jason 2026-06-10]
After every major revision cycle, a clean-context reviewer (no memory of the edits) reads the paper front to back as a first-time reader, hunting specifically for: logic holes and non-sequiturs; concepts used before they are introduced; numbers/claims updated in one location but not in their echoes (abstract ↔ intro ↔ body ↔ caption ↔ conclusion); narrative discontinuities left by section-local edits; references to figures/tables that changed meaning. Section-local resolution rounds systematically create these seams — the global pass is what closes them.

## Page-limit passes (measured, not vibes)
**Page budgets are FILL targets [rule, Jason 2026-06-10]: a stated content-page limit means filling those pages completely, never "under is fine"; for a 10-page-total paper, keep references ≤ 30 entries.** When under budget, the fill priority is new evidence (experiments, tables, verification figures) over prose padding.
Locate the overflow precisely (which page, how many columns of what). Then pull levers in order of information loss:
1. Font step-downs (displays, captions, tables, algorithms);
2. Subsection merges and redundant-proposition removal;
3. Targeted prose cuts (measured per-paragraph savings);
4. Float spacing (`\vspace` negatives, `\raggedbottom`);
5. Weakest-reference deletion — respecting a venue-citation floor (e.g., keep ≥8 target-venue refs).
Each step logged with its page impact and reversible.

## Rebuttal preparation
The anticipated-rebuttal stubs (from writing_assets) + the per-attack ablation figures (from the experiment plan) mean most reviewer attacks have a pre-built answer: scoping paragraph + a figure. Maintain that mapping explicitly (attack → remark → figure).
