# AI_STYLE_CHECKLIST — copy into each project; run as written
<!-- Origin: CDRO project (.agent/AI_STYLE_CHECKLIST.md), extended. Process rule is part of the checklist. -->

## PROCESS RULE (overrides everything)
**Propose-then-approve, one by one.** Run the sweeps, produce a NUMBERED list of candidate edits with before→after snippets, present to the owner, apply ONLY approved items. Never auto-apply. If an item holds up, say "fine" — no forced findings. Never add defensive/justification prose as a "fix".

## A. Grep token sweep (flag every hit; each hit = one numbered proposal)

| # | Pattern | Action |
|---|---------|--------|
| 1 | `—` em-dash as rhetorical glue (`---` in tex) | Restructure the sentence. (Proper-noun en-dashes are fine.) |
| 2 | `such as` | Ask: shorter / more concrete? Often deletable. |
| 3 | `not only ... but also` | Cap ~2/paper; prefer "both X and Y" or "X while Y". |
| 4 | `it is worth noting` `it should be noted` `in this regard` `from this perspective` `this observation is important` | Delete; state the content directly. |
| 5 | `enable` `facilitate` `leverage` `enhance` | Replace with the concrete verb (computes, outputs, reduces, selects…). |
| 6 | `comprehensive` `holistic` `seamless` `significant` `novel` `powerful` `flexible` `general` (as advertising) | Delete or replace with the specific property. |
| 7 | `framework` `paradigm` `mechanism` `module` `strategy` `scheme` (over-broad) | Replace with the concrete noun (controller, formulation, policy, method…). |
| 8 | `we aim to` `we seek to` `we attempt to` | Say what was done. |
| 9 | `in this paper, we propose` `the proposed` `robust and efficient` | Trim; state the result, don't advertise. |
| 10 | `not X, it is Y` / `The real problem is not A, it is B` | Rewrite. EXCEPTION: genuine mathematical disambiguation ("the set is not a product…, it is a single coupling") is exposition — keep. |
| 11 | Defensive hedging: `not a claim` `we do not (claim|interpret)` `this is not intended` `should not be (interpreted|read|taken)` `we make no claim` `we (emphasize|stress|caution)` `does not (imply|claim)`; `rather than` (any use) | Rewrite to plain statements of fact. `rather than` is BANNED outright [rule, Jason 2026-06-11]: restructure or split into two sentences; state the contrast positively ("learns from A, not B" or two sentences). The earlier methodological-contrast exception is revoked. |

## B. Read-level checks (whole-document pass)
1. Plain and understandable for a non-expert reviewer = top priority; no homemade jargon; define once in full, then use the short form.
2. No stacked abstract-noun strings ("uncertainty-aware safety-constrained grid-responsive flexibility management" → say what it does).
3. Sentence-template repetition (e.g., three colon-led "The result is X:" in a row) — vary or merge.
4. Template openers ("X is no longer just…", "This is both a challenge and an opportunity") and rhetorical flourishes ("cannot be an afterthought") — state the mechanism directly.
5. Front-to-back repetition; metaphor/adjective density; excessive passive voice.
6. Cut obvious transition sentences; don't wrap simple things in big words.
7. Contributions: specific, limited, credible — each maps to an existing theorem/figure.
8. Find paragraphs that preemptively defend against criticism; rewrite plainly; keep necessary limitations as plain statements.

## C. Worked transformations (calibration examples)
- "AI data centers are no longer passive consumers. As workloads… they are becoming…" → "As large-scale workloads expand, AI data centers are becoming large, fast-varying electricity loads." (template opener + merge)
- "This is both a challenge and an opportunity: uncontrolled growth can…, but properly controlled…" → "Uncontrolled growth can aggravate peak demand, while properly controlled loads can provide…" (template frame → direct contrast)
- "safety cannot be an afterthought: the limits define when…" → "the thermal limits define when demand can be shifted, so they must be enforced inside the controller." (flourish → mechanism)
- "we use these measurements only to verify feasibility rather than to claim a solver-speed advantage" → "Absolute runtimes depend on solver implementation; these measurements confirm real-time feasibility." (defensive → plain facts)
- "Two points are worth making explicit, because the construction is easy to misread." → "Two properties of (eq) deserve emphasis." (chatty/defensive → direct)
