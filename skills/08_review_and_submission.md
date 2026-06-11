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

## Algorithm boxes are code — audit them like code (PROSE Phase 7)
After rewriting a pseudocode box, re-derive its decision rules algebraically: a price/penalty term that is CONSTANT across candidates cancels out of an argmax (an `argmax (g_a − Q·c_a/V)/c_a` made the queue price algebraically inert — the controller's headline mechanism did nothing, contradicting the surrounding theorem; the fix moved the price into the stopping condition). Checklist per box: every symbol bound (REQUIRE or text), every variable assigned before use (a queue update referenced P(t) that nothing assigned), vector-vs-scalar bookkeeping consistent (a per-link slack vector had a scalar deducted), and comments use the paper's notation, not implementation slang.

## Triage reviewer comments: accept / accept-as-sentence / counter-strengthen / decline (PROSE round-4)
Not every comment deserves a fix — the owner's instruction "很多问题可能是吹毛求疵" licenses explicit verdicts. Four useful verdict classes: (1) ACCEPT with experiment — only for objections that change what the evidence shows (the round's one such item: a missing baseline class); (2) ACCEPT AS ONE SENTENCE — when existing data already answers it (a 3-decade sweep IS the ±1-decade sensitivity analysis; a pricing experiment already quantifies "how much of the gain comes from free slack"); (3) COUNTER-STRENGTHEN — when the complaint rests on a premise you can refute structurally: "optimality only within the periodic class" fell to a realization-independence argument (filter variance doesn't depend on measurements ⇒ every causal policy traces a deterministic schedule) plus a 200/200 numerical check, turning a scope apology into a stronger theorem-adjacent claim; (4) DECLINE with stated reason — research-scale asks (a Whittle-index baseline for a coupled problem), page-budget violations (symbol table), and submission-time mechanics (anonymization). Write the verdict table into the concern log so the decline reasons are auditable.

## A baseline's tuning curve can be its refutation (PROSE round-4)
When a simple competitor fails, sweep ITS knob before claiming victory — and when the whole tuning curve is dominated by a degenerate policy, say so: the variance-trigger rule at fast drift either over-triggers (any threshold below the stationary belief variance — burns all inventory, reward 0.25 vs floor 4.48) or never re-fires (any threshold at/above it — the belief approaches stationarity from below), so its BEST tuning equals never-probe. That one structural sentence converts "your baseline was mistuned" into "this rule class cannot ration, which is the paper's thesis." Bonus pattern: the collapse number itself (probe-everything → serve nothing) is the introduction's warning made quantitative — link them.

## Answer reviewer weaknesses with experiments, not only prose (PROSE round-3)
The two strongest reviewer objections ("the theorem's machinery is never exercised — decorative" and "your comparison confounds knowing-the-parameter with adapting") were both answerable with cheap targeted experiments rather than hedged rewording: (1) run the theory's machinery LIVE (hard-budget queue: show the constraint enforced, the O(V) backlog growing, the O(1/V) side saturating — three numbers kill the "decorative" charge); (2) implement the reviewer's hypothesized confounder as a BASELINE (the calibrated-schedule baseline = our own theorem run as a policy; it losing everywhere turned the attack into evidence FOR the adaptive mechanism). Heuristics: a reviewer-proposed baseline that embodies your own theory is the best kind — either it wins (theory matters) or it loses to your full method (the delta is exactly your contribution); when wiring a Lyapunov-style V knob into an experiment, CHECK UNITS first — a price term in surrogate units (nats) against costs in resource units made three decades of V identical (bang-bang granularity), and the meaningful V range was 100x higher than intuition.

## Page-budget endgame under float quantization (PROSE round-3)
When the last page is 1-2 lines over and prose trims stop moving the spill (float re-settling absorbs them), stop grinding sentences: (a) check the refs count against its CEILING — "<= 30" means 29 is legal, and absorbing one single-cite reference into a neighboring sentence is one clean entry (~4 lines); (b) global float-spacing knobs (\textfloatsep, table tail \vspace) buy ~10 lines in one edit; (c) a figure whose information fully lives in a table row is a 0.1-page cut with zero information loss. Track spill quantitatively (render last page, measure content pixels) — "still 11 pages" hides whether you are 2 lines or 30 lines away.

## Post-revision fresh-reader logic pass [rule, Jason 2026-06-10]
After every major revision cycle, a clean-context reviewer (no memory of the edits) reads the paper front to back as a first-time reader, hunting specifically for: logic holes and non-sequiturs; concepts used before they are introduced; numbers/claims updated in one location but not in their echoes (abstract ↔ intro ↔ body ↔ caption ↔ conclusion); narrative discontinuities left by section-local edits; references to figures/tables that changed meaning. Section-local resolution rounds systematically create these seams — the global pass is what closes them.

## Page-limit passes (measured, not vibes)
**Page budgets are FILL targets [rule, Jason 2026-06-10]: a stated content-page limit x is a range target — final content must land in [x, x+0.5] pages (e.g., INFOCOM 9pp content: between 9 and 9.5, the spill sharing the reference page); never under x. For a 10-page-total paper, keep references ≤ 30 entries.** When under budget, the fill priority is new evidence (experiments, tables, verification figures) over prose padding.
Locate the overflow precisely (which page, how many columns of what). Then pull levers in order of information loss:
1. Font step-downs (displays, captions, tables, algorithms);
2. Subsection merges and redundant-proposition removal;
3. Targeted prose cuts (measured per-paragraph savings);
4. Float spacing (`\vspace` negatives, `\raggedbottom`);
5. Weakest-reference deletion — respecting a venue-citation floor (e.g., keep ≥8 target-venue refs).
Each step logged with its page impact and reversible.

## Rebuttal preparation
The anticipated-rebuttal stubs (from writing_assets) + the per-attack ablation figures (from the experiment plan) mean most reviewer attacks have a pre-built answer: scoping paragraph + a figure. Maintain that mapping explicitly (attack → remark → figure).
