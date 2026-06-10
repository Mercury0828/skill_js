# Skill 02 — Authoring the project constitution (guide.md)

The constitution's quality is the single biggest determinant of how well autonomous execution goes. Budget real thinking time here; everything downstream is cheaper because of it. Quality bar: **a fresh agent reading only this file can run the project for weeks.**

## Required sections (battle-tested structure)

1. **One-paragraph pitch** + a frozen *framing line* (the talk/abstract soundbite). Write the soundbite on day 0 — it disciplines everything else.
2. **Canonical gap statement** — one paragraph, wording frozen, used everywhere verbatim. Must enumerate what each line of prior work does and does NOT do. Include a *wording-discipline note*: state exactly what the gap is NOT (the over-claim a careless writer would make), e.g., "the gap is not that nobody does X — it's the economics/optimality of X".
3. **Competitive landscape, two tables:**
   - Domain neighbors: per row — what they do / what they do NOT do (our delta) / their role for us (threat, baseline, lineage anchor, motivation). Mark rows needing primary-source verification as MUST-VERIFY with the exact question Phase 0 must answer and the expected answer.
   - Classical lookalikes a reviewer will pattern-match to ("kill proactively"): per row — why it looks similar / the memorized delta. Name the MOST DANGEROUS one explicitly.
4. **The paper's Table 1 prototype** — an information-structure / capability table with binary dimensions where your work is the unique all-yes row. Designing this table IS designing the contribution.
5. **Locked modeling decisions** (numbered, with rationale, dependencies, and the attacks each defuses). Separate: in-scope / out-of-scope-one-remark-each / journal-version reserve ammunition. Locked = not reopened without owner escalation.
6. **Working formalization v0.x** — enough notation and structure for theory/sim phases to start; mark what the agent may refine vs what requires escalation.
7. **Theory roadmap, two tracks:** SAFE track (must land; alone publishable) and BONUS track (ceiling-raiser) with a **pre-committed downgrade trigger** ("if not clean after N focused weeks → fallback X"). For each result: the sketch, the deliverable, and **known traps with fallbacks** (e.g., "submodularity holds statically, NOT sequentially — scope the claim"). Mark all sketches as claims to re-derive, and state the agent is rewarded for finding sketch errors.
8. **Experiment plan:** simulator module layout; the full policy/baseline list (name the baselines after the prior work they implement — "X-style"); metrics; **killer figures F1–Fn with their predicted qualitative shapes** (a figure contradicting its predicted shape = escalation, maybe a finding, never silently forced); parameter-calibration plan tied to published measurements.
9. **Phase plan** — ordinal phases, each with embedded acceptance criteria (trend-matching unless a constant is pinned), each ending with a phase report + git tag. Include a mid-project SHOWABLE ARTIFACT milestone (self-contained walkthrough someone external could inspect).
10. **Risk register** — named risks with levels and concrete triggers/mitigations (scoop risk gets a re-sweep cadence; premise attacks get their defusing decision + ablation figure).
11. **Writing assets** — title candidates, contribution statement drafts, quotable lines, anticipated-rebuttal stubs. Collected from day 0.
12. **Repo conventions** + operating rules.
13. **Appendices: verbatim seeds** for `PROJECT_STATE.md` and `DESIGN_DECISIONS.md` (so bootstrap is copy-paste, not interpretation) + a notation/glossary freeze.

## Authoring heuristics

- Every "we'll figure it out later" in a guide becomes an agent stall or a bad silent assumption. Pre-decide or pre-delegate ("agent may refine constants; structural changes escalate").
- Phrase acceptance criteria as *observable artifacts* ("file X exists with property Y verified by Z"), not intentions.
- Embed the expected answers to MUST-VERIFY questions — being wrong then triggers escalation, which is exactly the safety you want.
- The classical-lookalikes table is reviewer-defense work done early; one transplanted baseline from the most dangerous lookalike answers "old wine" with data instead of prose.
- Write one sentence delimiting against your own sibling projects before a reviewer does.
