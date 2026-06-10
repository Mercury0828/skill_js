# Skill 09 — Tooling gotchas (hard-won, mostly Windows)

## PDFs
- Many arXiv PDFs carry an **encryption flag** that makes PDF-reading tools refuse them ("password-protected") — the files are fine; extract text with `pdftotext` (poppler). `pdftotext` without `-layout` handles two-column papers acceptably; grep the txt for model keywords, then read targeted line ranges.
- **Verify every downloaded PDF with `pdfinfo`** — paywalled endpoints (IEEE iel8, Optica viewmedia, ResearchGate) return HTML/JS-challenge pages that save as `.pdf` and even pass casual inspection by size.
- Wiley/IET `pdfdirect` and Optica fulltext are typically 403/JS-gated to scripts even when the article is open access in a browser — log the trail, ask the owner for an institutional download, move on.
- Wayback Machine captures of author copies can be 403 "capture excluded" — check scholar.archive.org for the snapshot ID anyway (proves existence, helps the owner find it).

## Git on Windows
- `.gitattributes` with `*.pdf binary` (and parquet/pkl/png) BEFORE committing binaries — autocrlf treats an HTML-masquerading-as-PDF as text and corrupts it; you'll see "LF will be replaced by CRLF" warnings on a .pdf, which is the red flag.
- Pre-existing remote with an initial commit: `git pull origin main --allow-unrelated-histories --no-edit`, then push — don't force-push over an owner-created README.
- Empty skeleton dirs need `.gitkeep` placeholders.
- Set committer identity per-repo or per-command (`-c user.name=... -c user.email=...`) when the global config may differ across machines.

## PowerShell 5.1 quirks (when not using bash)
- No `&&`/`||` chaining; use `;` or `if ($?)`. No ternary/null-coalescing.
- `Invoke-WebRequest` needs `-UserAgent "Mozilla/5.0"` for many academic hosts; errors are localized (e.g., Chinese "(403) 已禁止"), match on status codes not strings.
- Default file encoding is UTF-16; pass `-Encoding utf8` when writing files other tools will read. Prefer the bash tool for POSIX one-liners (grep/sed/pdftotext loops).

## Subagent orchestration
- Background agents must NOT write shared .md files (the orchestrator assembles); give them disjoint download targets and a structured-report final-message contract.
- Each agent prompt carries: 3-line project context, exact per-item output format, naming convention, and the "final message is consumed programmatically" line — otherwise you get prose summaries instead of data.
- Spot-check any agent-supplied quote that carries decision weight against the source text yourself.

## Polytope / optimization libraries (ENCORE Phase 2)
- `pypoman.project_polytope(method="bretl")` asserts `eq is not None` — for pure-
  inequality systems, append a dummy variable pinned to 0 by one equality; Bretl–Lall
  then works and scales with OUTPUT complexity (vertices of the 2-D shadow), not input
  dimension — 14-D lifted systems project in ~0.2 s. The cdd path
  (`project_polyhedron`) returns duplicated vertices; dedupe before hulling.
- `scipy.spatial.ConvexHull.equations` gives H-reps ([A, -b] rows) and `.volume` is
  AREA in 2-D — cheap membership tests and polygon metrics without extra deps.
- Empty/degenerate projection slices (infeasible parameter combos) are data, not
  errors: catch the exception, store an explicit empty marker, and report the count —
  silent exclusion reads as coverage.

## Web fetching
- arXiv HTML (`arxiv.org/html/<id>` or ar5iv) beats PDF extraction for targeted Q&A on recent papers.
- Semantic Scholar API rate-limits (429) without a key; Unpaywall API is a reliable open-access checker.
- Author homepages (`~author/PUBLICATION/` paths) are the highest-yield source for paywalled venue papers; same-author theses reproduce paywalled models legitimately (flag the substitution).
