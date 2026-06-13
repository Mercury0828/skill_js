# Skill 10 — Paper production pipeline (frozen-results → submission-ready draft)

Distilled from the WEFT INFOCOM run (2026-06-13), where a 10.1-page draft went from
zero to a 4-reviewer-audited revision in one session. Complements 07 (style system)
and 08 (review mechanics); this file is the ORDERING and the gates.

## Phase W0 — Preconditions (do not start writing without these)
- Experiments FROZEN under a tag; every result number lives in a committed artifact
  (arrays + expected.md outcome addenda + FINAL_REVIEW table). Writing from prose
  memories of results is how number drift starts.
- refs.bib resolver-verified (arXiv API / Crossref) BEFORE drafting: write
  `check_refs --online` style gating early; never let an unverified entry in. Add the
  classical/theory anchors in one batched verification session.
- A reference paper from the same owner/venue family, read for: section skeleton,
  float style, caption norms, theorem/proof placement, and the owner's standing
  style rules (copy its AI_STYLE_CHECKLIST.md into .agent/ and APPLY THE EVOLVED
  COPY, not the template — the project copy carries owner rulings the template lacks).

## Phase W1 — Draft order [rule]
Write in this order: model → theory → synthesis/method → evaluation → related →
INTRO (contributions last among body) → conclusion → ABSTRACT (always last).
Rationale: contributions must map 1:1 to theorems/figures that already exist in the
draft; abstracts written first always overclaim. Every number typed into prose is
copied from the frozen artifact AT THAT MOMENT (open the file, don't recall it).

## Phase W2 — Page budget as a fill target [rule, owner standing]
The stated limit x is a RANGE target [x, x+0.5] (WEFT: >10 and <=10.5). Compile
EARLY and often; floats absorb ~0.5-1 page of additions silently, so measure with
rendered last-page fullness (pdftoppm), not page count alone. When under target,
fill priority is NEW EVIDENCE: an algorithm box, a workload/parameter table, formal
propositions with inline proofs, a secondary-scale figure — never prose padding.
Page-cut levers (when over) are in skill 08.

## Phase W3 — Per-batch style gates (07's system, applied)
After each section batch: token sweep (expect ZERO hits if you wrote with the rules
in force — a nonzero sweep on fresh prose means you drafted on autopilot), acronym
discipline sweep in READING order (the classic violations: re-defining in Sec. II
what the intro defined; using a coined family name in Sec. III that Sec. IV
defines; once-only acronyms), and a cross-location number echo check
(abstract = intro = body = table = caption = conclusion).

## Evaluation prose = analysis, not narration [rule, owner standing, WEFT 2026-06-13]

The figure or table carries the NUMBERS; the prose must carry the WHY. The
common failure is evaluation text that narrates the artifact —"DLS reaches
$\alpha_c=0.25$ on QFT and a worst-case regret of 38%"— which has zero marginal
value because the reader already sees the table. Owner ruling: "实验结果分析
经常会写成图表的内容复述，没有一点深度，这很不好。应该多一些有深度的分析，
少一些数据结果陈述。删掉的数据结果陈述可以留空间给更多实验结果."

What evaluation prose must contain instead, per result:
- MECHANISM: why this fabric wins this workload (DLS's adjacent-group ring turns
  the dragonfly's single inter-group hop into a parallel short path exactly
  where banded demand concentrates).
- IMPLICATION: what it means for the design decision (so a deployment expecting
  hub/band traffic should buy ring augmentation, not bisection).
- CONNECTION: tie back to theory/the law/the cost trade (the winner moves with N
  exactly as $\eta^\ast(N)$ predicts).
- SURPRISE: where intuition or the prior fails (the worst cut is ball-shaped,
  not the symmetric cut classical bisection would pick).

The deletion test: strike every sentence that would still be true if the reader
saw only the table. If little survives, the paragraph was narration — rewrite it
as the four items above. The numbers stay in ONE place (the float); cite them in
prose only when the analysis turns on a specific value.

This compounds with the figures-over-prose rule: when over the page budget, cut
the NARRATION sentences, not figures — "图有些少了，文字有些多了" (owner). A
systems paper persuades visually; the freed space buys MORE EVIDENCE (another
scale, an ablation, an execution-time validation), which is worth more than any
amount of restated prose. Less narration + deeper analysis + more experiments is
the same move three times.

## Phase W4 — Multi-reviewer simulation (the core quality mechanism)
Launch 4+ one-shot clean-context reviewers IN PARALLEL with disjoint mandates and
structured-table output contracts:
1. DATA INTEGRITY with artifact paths and the explicit mandate "re-derive from the
   arrays, do not trust the prose" — in WEFT it recomputed npz files and caught the
   paper citing a superseded grid's narrative against its own shown figure, a
   46%-vs-42% load-point swap, and a phantom artifact file.
2. MATH/PHYSICS with the repo's theory notes and code as ground truth — caught a
   missing premise in a one-line proof (with a counterexample) and a circular
   two-step dependency in a hardness ledger.
3. TPC/OVERCLAIMS (venue persona, accept/reject lens) — caught the seeded-discovery
   narrative ("synthesis discovers X" where X was hand-authored into the grid after
   the augmentation hint) and the all-in-house-candidates fairness hole.
4. STYLE + FRESH-READER (no memory of writing) — catches cross-section seams:
   dangling labels from cut drafts, count mismatches ("five families" listing six),
   concepts used before definition, caption-only definitions.
Reviewer lenses catch DISJOINT A-issues (WEFT: near-zero overlap across 61 concerns).

## Phase W5 — Freeze, triage, respond [rule]
Freeze ALL concerns in one table (paper/REVIEW_roundN_concerns.md) before fixing
anything; assign each a verdict: ACCEPT / ACCEPT-AS-SENTENCE / COUNTER-STRENGTHEN /
DECLINE(stated reason) / ACCEPT-WITH-EXPERIMENT. Two standing rules:
- Evaluation-scale and fairness objections get EXPERIMENTS, not wording: WEFT added
  a random-graph (Jellyfish-class) candidate family, re-ran two scales, and ran the
  robust-selection machinery at the largest scale — the robust conclusion surviving
  a new external baseline is worth ten defensive sentences.
- Never claim an in-flight experiment's result in prose. Write the scoped-down
  sentence now ("at 16 and 64 modules"), upgrade only after the run lands.
Number-conflict concerns usually mean BOTH numbers are real but from different
bases/grids (pre- vs post-enrichment; gain-over-base vs gap-vs-exact): the fix is
naming the base explicitly, not picking one number.

## Phase W6 — Re-audit loop
After the fix round: full recompile (check pages stayed in [x, x+0.5], zero
undefined refs, overfull boxes < ~20pt), regenerate any figure whose source data
changed, then a FRESH clean-context fresh-reader pass over the revised paper.
Iterate W4→W6 until a round produces no A/B-level concerns; only then notify the
owner for acceptance.

## Mechanics that saved time
- main.tex + sections/*.tex inputs; latexmk; gitignore the intermediates DAY ONE.
- PowerShell-native quoting eats double quotes in commit messages and `-replace`
  on multi-line LaTeX is fragile — prefer the editor tool for any replacement
  spanning lines; verify the file after every regex edit.
- TikZ system figure beats importing a draw.io PNG: it inherits the paper's fonts
  and is fixable by the same review loop.
- Keep the experiment runners' `--config=` and `--plot-only` switches: reviewer
  responses become one-line reruns instead of new scripts.

## Reference replication is a DISTINCT TASK TYPE [rule, learned the hard way on WEFT 2026-06-13]

When the owner names a reference paper to follow ("参考这篇论文的写法、章节分布、
组件内容"), the task is STRUCTURE REPLICATION, not free generation. Success means
matching the reference's structure and components, not producing a reasonable
paper. The reference overrides your generic "what a conference paper looks like"
prior. On WEFT, missing this cost a full structural rewrite after the owner
returned 10+ corrections; the failure traced to five stacked causes, root first:

- ROOT: misclassified the task as free generation, so I judged the draft by "is
  this a reasonable INFOCOM paper?" (yes) instead of "does this mirror the
  reference's structure?" (no). Every other cause is a symptom of this one.
- Overrode the explicit instruction with a generic prior (treated my default as
  more authoritative than the owner's example).
- Trusted memory of the reference instead of a line-by-line component checklist
  (the same "never trust prose memory" rule I enforce for result numbers, not
  transferred to writing).
- Optimized "page-limit compliance" (compress, omit components) instead of "match
  the reference's density" (fill, build components) — the page limit is a FILL
  target [x, x+0.5], never a ceiling to satisfy by compressing.
- Skipped a pre-writing alignment checkpoint, so the structural mismatch surfaced
  only in review when a full draft already existed.

MANDATORY ordered steps when a reference is named:
1. RECLASSIFY out loud: success = matching the reference; the reference beats your
   prior; deviations need the owner's sign-off.
2. READ EVERY SECTION FILE of the reference (system model, methodology,
   experiments), not just main.tex + intro — the structure lives in those files.
3. BUILD A COMPONENT-MAPPING TABLE (reference component -> our instance) covering:
   intro subsections + literature review + positioning table; each body section's
   subsection count and page length; a MAIN all-baselines result table; a FORMAL
   proof under every theorem/prop (never a "sketch" if the reference proves in
   full); figure TYPES (match the mix — if the reference uses line/schematic
   figures and ZERO heatmaps, do not substitute heatmaps); related-work PLACEMENT
   (CDRO put it inside the intro, not a late standalone section); experiment-SETUP
   depth (environment, data, baselines, protocol — CDRO's setup names the
   implementation, run times, operating ranges, plant params, and EVERY baseline);
   page fill to [x, x+0.5] using the reference's DENSITY as the baseline.
4. CONFIRM THE MAPPING WITH THE OWNER before writing prose (pre-writing alignment
   checkpoint); raise any intended deviation here, not in review.
5. TICK THE TABLE mechanically while writing; never rely on memory that a
   component was covered.

The protocol costs ten minutes of outlining; skipping it cost a full structural
rewrite (intro doubled, Section II expanded, main result table built, T1 proof
formalized, related work folded into the intro, heatmaps cut, topology schematic
added, experiment setup quadrupled). That asymmetry is the rule.
