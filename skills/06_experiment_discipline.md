# Skill 06 — Experiment discipline & artifact integrity

## Reproducibility [rule]
- Config-driven runs: every figure reproducible from `experiments/<name>/config.yaml + run.py`. No notebook-only results.
- Seeds fixed and logged; [default] ≥20 seeds, mean ± 95% CI, warm-up discard; state the seed count in the paper and flag every exception explicitly ("N seeds unless noted otherwise" + the note where it differs).
- Results dir git-ignored except summary csv/png; figure-generating code tracked from the moment it exists.

## Simulator-vs-theory unit tests (acceptance criteria, not afterthoughts)
The simulator must reproduce the theory it will test: estimator-variance formulas within CI across the parameter range; stationary distributions (KS test); posterior calibration (empirical coverage of 90% credible intervals ∈ [88%, 92%] over long runs); composition/conservation laws. These tests gate the simulator phase.

## Posterior-calibration coverage tests catch estimator bugs nothing else catches (PROSE Phase 3)
A "90% credible-interval empirical coverage ∈ [88%, 92%]" unit test on the full filter pipeline caught three real bugs in one session, none visible in variance-formula tests alone: (1) simulation params violating the model's own validity stipulation (state pinned at a clip boundary); (2) plug-in variance labels collapsing to zero at a boundary outcome (estimate=perfect ⇒ label=0 ⇒ filter overconfident); (3) **label–noise correlation bias** — any measurement-variance label computed from the noisy realization itself over-trusts upward-noisy readings and biases the posterior (~0.6σ); fix = certainty-equivalence labeling (evaluate the label at the filter's predicted mean, not at the estimate). Debug coverage failures quantitatively: compute empirical z-scores (error/posterior-sd); z-mean ≠ 0 means bias (look for label or model asymmetries), z-sd ≠ 1 means mis-scaled variance. Document the resulting operating envelope (e.g., minimum batch size) as a design constraint for downstream components.

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

## Place experiments ON the theory's regime map (PROSE Phase 4)
When a baseline you expected to lose is winning, first check whether the config sits in a theory-predicted degenerate regime — the first PROSE smoke landed exactly in the derived never-probe region, so "no differentiation" was a *validation*, not a failure. Use the theory to PLACE the experiment: compute the geometry that makes the interesting behavior possible (e.g., truth-variability > decision-margin > achievable-estimate-precision, with the arithmetic in the config comments), and keep one degenerate-regime point in the final sweep as an anchor (it shows the theory predicting its own baseline's success). Corollary rules: (1) honest-baseline tuning — set each baseline to its best plausible parameters before comparing (a mistuned trigger threshold = strawman); (2) when a resource is perishable, opportunity cost is a shadow price (displaced demand), not a list price — naive per-unit pricing makes optimal policies look absurdly conservative; metrics must then separate "consumed slack" from "displaced service".

## Calibrate ablation grants in the paid alternative's units (PROSE Phase 5)
When an ablation GRANTS a baseline some free capability ("what if they had feedback?"), quantify the grant in the same units as the paid mechanism it substitutes — an over-generous grant silently flips the conclusion. First F4b draft granted feedback equivalent to a free 60-pair tomography batch per path per slot (and on ALL paths, breaking the very one-sidedness being studied): baseline "won". The physically-calibrated grant (signal only from units actually served-and-committed, confounded noise at realistic magnitude, delayed) restored the true structure — and surfaced a bonus mechanism (one-sided feedback can't bootstrap: you only learn about what you already trust). Rule: write down the grant's information content (variance per slot, equivalent paid units) in the runner's docstring before running.

## Sweep design under saturation constraints (PROSE Phase 5)
When the state variable saturates (here w ≤ 1), a single-knob sweep (intensity q at fixed reversion κ) silently exits the model's validity region at one end. Joint sweeps that hold an invariant fixed (constant stationary amplitude: κ ∝ q) keep every point valid and often produce a cleaner x-axis ("drift RATE at fixed wander amplitude"). State the invariant in the config comments and report the sweep design as a logged decision.

## Robustness & ablation patterns
- Misspecification test: ground truth from a richer process than the model assumes (e.g., regime-switching truth vs smooth model) — show graceful degradation.
- One ablation per anticipated reviewer attack, planned in the guide (the ablation IS the rebuttal).
- Sweep grids logged in configs; bracket published real-world parameter ranges so headline plots are anchored in measured territory.
