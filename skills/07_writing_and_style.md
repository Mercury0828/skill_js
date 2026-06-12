# Skill 07 — Writing & the anti-AI-flavor system

The operational checklist lives at `templates/AI_STYLE_CHECKLIST.md` — copy it into each project and run it as written. This file explains the system around it.

## Collect writing assets from day 0
`docs/writing_assets.md` accumulates: frozen gap sentence, framing soundbites, quotable theory lines, title candidates, contribution-statement drafts, anticipated-rebuttal stubs. Phases ADD to it (a good quotable line discovered during theory work goes in immediately). Writing the paper then starts from assets, not from a blank page.

## The two-level anti-AI-flavor method
1. **Grep token sweep** — mechanical pass over banned/flagged tokens (em-dash glue, "such as", "not only…but also", transition fluff, vague verbs enable/leverage/facilitate, empty adjectives comprehensive/novel/seamless, over-broad nouns framework/paradigm/mechanism, "we aim to", the "not X, it is Y" construction, defensive hedging). Every hit becomes a numbered proposal.
2. **Read-level checks** — repetition of sentence templates, stacked abstract-noun strings, metaphor/adjective density, passive-voice excess, template openers ("X is no longer just…"), advertising tone in contributions, defensive paragraphs. Plain-and-understandable-for-a-non-expert is the top priority.

## Style-sweep failure modes caught by the owner (PROSE Phase 7) [rule]
1. **The sweep is per-batch, not per-paper.** Every batch of NEW prose (revision rounds, added paragraphs, rewritten abstract) gets its own checklist pass before commit. A one-time sweep early in writing left 45 em-dashes in the final draft because later rounds kept adding them — the owner caught it from the abstract alone.
2. **Em-dash bar is near-zero, parenthetical pairs included.** A lenient audit ("most are legitimate paired insertions") is wrong: the owner's standard treats `---x---` pairs as the primary AI tell. Replacements: paired → commas or parentheses or sentence split; single → colon or comma. Legitimate exceptions only: table N/A cells, code comments, proper-noun en-dashes (Ornstein--Uhlenbeck, Cauchy--Schwarz).
3. **Inline proofs are part of venue style.** If the reference paper puts `\begin{proof}` blocks right after every theorem/prop/lemma, do the same from the first draft — retro-fitting nine proofs costs a page of budget juggling.

## Process rules for style editing [rule]
- **Propose-then-approve, one by one.** Numbered list with before→after; apply ONLY what the owner approves. Never auto-apply rewrites.
- **No nitpicking:** if a checked item holds up, say "fine"; no forced findings; prefer one-line surgical edits.
- **Never add defensive/justification prose** to answer a critique — hedging is itself an AI tell and introduces new errors. State facts plainly; keep necessary limitations as plain statements.
- **Respect the reword bound:** if it's already clear, leave it. (The "AI reword spiral" — each pass making prose worse — is real and observed.)
- "rather than" is BANNED outright [rule, Jason 2026-06-11]: restructure or split into two sentences; state the contrast positively ("learns from A, not B" or two sentences). The earlier methodological-contrast exception is revoked.

## Captions: minimal [rule, Jason 2026-06-10 — supersedes the earlier "what/how/takeaway" reading]
Figure and table captions are SHORT — typically one sentence stating what is shown plus the conditions (seeds, axes, special markers); at most two sentences when a table needs a bold/dash legend. Takeaways, mechanisms, and numbers belong in the body text, never in the caption. When trimming an over-long caption, first move any caption-only fact into the body (don't delete evidence), then cut.

## Structural writing rules
- The strongest neighbor gets invited in and killed by us, in our words, with a table and a transplanted baseline — never left for Reviewer 2 to discover.
- Narrow gap statements are assets, not weaknesses: "practitioners already do X ad-hoc; the theory of X does not exist" is the best motivation structure available.
- One remark maximum per out-of-scope concern (the guide pre-writes these remarks); scope creep in prose is as real as in code.
- Contribution statements: specific, limited, credible — each maps to a theorem/figure that exists.

## Cross-document consistency (end of writing phase)
Tables ↔ figures ↔ prose ↔ abstract ↔ conclusion numbers reconciled in one dedicated sweep; every number in prose traced to its generating artifact.
