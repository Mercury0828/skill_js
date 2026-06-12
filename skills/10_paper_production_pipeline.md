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
