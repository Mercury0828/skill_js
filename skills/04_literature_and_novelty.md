# Skill 04 — Literature acquisition & novelty verification (the Phase-0 playbook)

Phase 0 gates everything: if the gap statement is wrong, every later phase is wasted. Battle-tested workflow (PROSE, 2026-06: 23 papers, 5 verdicts, 1 escalation, ~1 session).

## Principles
- **Model-level extraction, not abstract-level.** Per paper record: their state / decision variables / observation model / objective; verbatim quotes (≤15 words each, ALWAYS with section pointers) of the load-bearing assumptions; a one-line delta. Abstract impressions are not evidence — verdicts quote primary sources or say UNRESOLVED.
- **The verdict file is the gate.** For each closest neighbor: an explicit gating question ("does it model X under Y?"), verdict ∈ {NO, PARTIAL, YES} with a sub-question table (each axis answered + quoted). YES or strong-PARTIAL → `ESCALATION REQUIRED` header + open_questions entry; finish the phase regardless.
- **A strong-PARTIAL on a sub-axis re-scopes wording, not the project.** Record the precise cut ("cite prominently, differentiate on axes A/B/C, never claim D") as a binding for later phases.
- **Every guide row ends as COVERED or NOT-OBTAINED-with-trail.** A trail = the queries/URLs tried and why each failed (paywall, 403, JS-gate, no arXiv). NOT-OBTAINED is acceptable; silence is not.

## Execution pattern (parallel fan-out)
- Handle the **gating neighbors yourself** (the ones whose verdicts decide the project); fan out background subagents for supporting groups (lineage anchors, primitives, classical lookalikes, quantitative-evidence sweeps).
- Subagent prompt must specify: project context in 3 lines; per-paper extraction format (biblio / model / quotes ≤15 words + pointers / delta / numbers / download status + trail); download target dir + naming convention (`<ID>_<firstauthor><year>_<topic>_<arxivid>.pdf`); "your final message is consumed programmatically — return full structured reports"; "do NOT edit repo .md files" (the orchestrator assembles, avoiding write conflicts).
- Orchestrator assembles the dossier, writes all verdicts, and spot-checks agent quotes that carry weight.

## Acquisition tactics (see also skills/09 for tooling)
- arXiv PDF direct; author homepage copies (search `"<title>" pdf <author> <institution>`); ar5iv / arxiv.org/html for full-text reading; institutional repositories/theses reproducing the same model when the paper is paywalled (a same-author thesis chapter is a legitimate model source — flag it as such).
- Verify EVERY downloaded PDF with `pdfinfo` — paywalled endpoints return HTML/JS pages saved as `.pdf` (observed; they then get text-mangled by git too).
- Log venue-only candidates (IEEE-paywalled, no preprint) as UNRESOLVED with abstract-level provisional assessment — never assert a verdict you can't quote.

## Candidate identification (when the exact citation is unknown)
Search multiple phrasings + venue programs; list top-3 candidates ranked with one-line descriptors; adopt the best provisionally, flag for owner confirmation, and write the verdict for each candidate separately (they may have different information structures).

## Quantitative-evidence sweeps (parameter calibration)
When the model needs real-world parameter ranges: collect ≥4 published quantitative sources across ≥3 categories; per source record the exact number + units + quote + figure/section pointer, then show the conversion arithmetic to model parameters explicitly (order-of-magnitude honesty; trend > constants). The paper sentence this buys: "parameters calibrated to published measurements." Sweep grids should bracket the published range so the money plot's x-axis is anchored in measured territory.

## Standing afterward
- Quarterly novelty re-sweep reminder in PROJECT_STATE (re-run the Phase-0 searches; watch the named rival lines). [default: quarterly]
- Table-1 draft maintained with a citation on every row and a uniqueness self-check; structural refinements vs the guide prototype are allowed when evidence demands, but logged as deviations.
