# Skill 05 — Theory verification

## Stance [rule]
All sketched derivations (from supervisor/owner/prior notes) are **claims to re-derive from scratch**, not ground truth. The agent is rewarded for finding sketch errors — report them, never paper over. Trend-matching is the acceptance bar; sketched constants are expected to be sloppy.

## Two independent checks per closed form [rule]
1. **Symbolic** (sympy or hand derivation written out in `theory/`).
2. **Numerical** (Monte Carlo within CI; for filters/processes, exact recursions — e.g., Riccati — as cross-check).
A formula enters the paper only after both pass; the verification notebook/script is a tracked artifact reproducing every formula.

## Traps & fallbacks, pre-declared
- Write known traps INTO the guide with their fallbacks before attempting proofs ("X holds in the static case, NOT automatically sequentially — scope the claim to static; fallback: surrogate Y").
- Never claim an unverified property; "verified within scope S" beats "holds" every time.
- Confine guarantees to the tractable regime explicitly (the classes of structure you can actually prove things in); do not promise bounds in known-intractable territory — one over-claim can sink the paper.
- For conjectured structural properties: symbolic attempt + **numerical counterexample search over random instances** before believing either direction. A found counterexample is content (document it).

## Cross-check every quantitative claim against governing laws
Real failures caught this way (CDRO): a complexity claim missing a per-iteration assembly term; an energy claim violating a cube law (3× claimed, 8× actual); a storage claim requiring a physically impossible temperature swing. Habit: for each number or scaling in prose, ask "what law generates this?" and recompute once from that law.

## Approximation honesty
State every approximation where it is introduced (Gaussian noise on transformed variables, quadratic loss around a threshold, deterministic cost in the main theorem with the stochastic version as corollary). Honest scoping is also reviewer defense: the prepared one-remark for each simplification goes in the guide's locked-decisions section.

## Bookkeeping
Propositions/theorems numbered to match the eventual paper skeleton; notation table frozen at the consolidation phase; derivation files in `theory/` named by result number.
