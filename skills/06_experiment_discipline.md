# Skill 06 — Experiment discipline & artifact integrity

## Reproducibility [rule]
- Config-driven runs: every figure reproducible from `experiments/<name>/config.yaml + run.py`. No notebook-only results.
- Seeds fixed and logged; [default] ≥20 seeds, mean ± 95% CI, warm-up discard; state the seed count in the paper and flag every exception explicitly ("N seeds unless noted otherwise" + the note where it differs).
- Results dir git-ignored except summary csv/png; figure-generating code tracked from the moment it exists.

## Simulator-vs-theory unit tests (acceptance criteria, not afterthoughts)
The simulator must reproduce the theory it will test: estimator-variance formulas within CI across the parameter range; stationary distributions (KS test); posterior calibration (empirical coverage of 90% credible intervals ∈ [88%, 92%] over long runs); composition/conservation laws. These tests gate the simulator phase.

## Baseline hygiene
- Name baselines after the prior work they implement ("X-style periodic", "Y-style fixed-fraction") — every named baseline doubles as a citation and a rebuttal.
- Include: an oracle upper bound, a degenerate lower bound (never-act), the natural heuristic, and one baseline transplanted from the most dangerous classical lookalike (answers "old wine" with data).
- Add honesty knobs that make weak baselines non-strawman (sweep the parameter that would save them; show where it does and doesn't).
- Sanity orderings (oracle ≥ ours-full ≥ ours-reduced ≥ best heuristic ≥ degenerate) are smoke-test acceptance criteria; violations are investigated and classified (bug vs finding) before proceeding.

## Table & figure integrity (anti-fabrication; CDRO hard lessons)
- **Sanity-print:** figure-generating code prints the table values it must match; correspondence verified programmatically, not by eye.
- **Per-cell invariant checks** on every results table: consistency identities (flag A > 0 iff condition B), monotonicity where the model implies it, arithmetic recomputed row-by-row, cross-table totals reconciled.
- **Statistical plausibility:** a zero-violation mean sitting < 2.5σ from its limit is implausible; error bars must survive a reviewer's σ-arithmetic.
- **No suspicious roundness:** values all on a 0.05 grid read as fabricated; real pipelines produce irregular digits.
- **Figures:** regenerate from tracked code only (never hand-edit an image); render at 300 dpi and visually inspect for overlaps/clipping/label collisions before declaring done; match sibling-figure aspect ratios by MEASURING axes boxes, not eyeballing.

## Robustness & ablation patterns
- Misspecification test: ground truth from a richer process than the model assumes (e.g., regime-switching truth vs smooth model) — show graceful degradation.
- One ablation per anticipated reviewer attack, planned in the guide (the ablation IS the rebuttal).
- Sweep grids logged in configs; bracket published real-world parameter ranges so headline plots are anchored in measured territory.
