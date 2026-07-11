# CANDIDATES

Tool/rule candidates under the tool philosophy. Candidates are **distilled from
observed recurring real bugs** (the gift-PR fleet) — not invented. A pattern
becomes a candidate here when first noticed; it ships only when it clears the
gates below.

## The discipline (load-bearing)

1. **Recur-before-build.** A pattern is not built into a *default*-tier rule until
   it has **≥3 real upstream instances** (merged fixes, or open PRs with
   maintainer engagement). One instance is an anecdote; recurrence is evidence.
   Below threshold → `pedantic` (opt-in) or `needs-more-evidence`, never default.
2. **Two-gate at build time** (formalized as ToolUse + ToolUseEcosystem):
   - **ToolUse gate** — real ΔU (catches a bug that matters), and near-zero false
     positives on clean code. A noisy rule is rejected, not tuned down silently.
   - **Ecosystem gate** — narrow, evidence-driven, non-redundant (no existing
     tool, off-the-shelf or in this family, catches it), no feature creep.
3. **One tool per problem class.** If two converge on the same corpus, fold
   (cf. aibug-gate → wildlint). The family stays non-redundant.

A pattern that recurs but can't be made low-noise is logged in **Rejected** below
— that negative space is the proof of selectivity (cf. wildlint's "bugs
considered but not shipped").

## Entry format

- **Pattern** — the bug class, concrete.
- **Instances** — real upstream fixes (`repo#PR`, status). Count must reach ≥3 for default.
- **ΔU** — why it matters (severity / what it prevents).
- **Precision** — can it be near-zero-FP? (the decider)
- **Verdict** — `build (default)` / `build (pedantic)` / `needs-more-evidence` / `rejected-not-shippable` / `redundant (cite tool)`.
- **Target** — where it lands (wildlint WL/WP, mcp-lint, agent-wall, …).

---

## Current candidates

### From the aibug-gate fold → wildlint (see wildlint#15)
Each rests on ~1 upstream instance — below the recur-before-build threshold for
*default* tier. Honest tiering: ship as `pedantic` (as aibug-gate already had
most of them), or gather more evidence before default.

- **`str.split(' ')` vs `str.split()`** — stray empty tokens.
  - Instances: derek73/python-nameparser#164 (merged). [1/3]
  - ΔU: medium (silent wrong parse). Precision: feasible (literal `' `' arg).
  - Verdict: **build (pedantic)** → wildlint.
- **`not A and B or C` precedence** — `and` binds tighter than `or`.
  - Instances: alexanderlukanin13/coolname#34 (open). [1/3]
  - ΔU: low. Precision: needs paren recovery (token stream).
  - Verdict: **build (pedantic)** → wildlint.
- **radix/length from original param after an override guard** — silent wrong values.
  - Instances: skorokithakis/shortuuid#115 (merged). [1/3]
  - ΔU: high. Precision: feasible but narrow.
  - Verdict: **needs-more-evidence for default; pedantic meanwhile** → wildlint.
- **log-derived exponent + rounded mantissa, no carry-guard** ("1000.0 kB").
  - Instances: python-humanize/humanize#329 (merged). [1/3]
  - ΔU: medium (display). Precision: feasible (humanizer call shape).
  - Verdict: **build (pedantic)** → wildlint.
- **magnitude-binning loop breaks on `<=` at boundary** (1024 → "1024B").
  - Instances: mahmoud/boltons#403 (merged). [1/3]
  - ΔU: medium (display). Precision: feasible.
  - Verdict: **build (pedantic)** → wildlint.

### Needs more evidence
*(add patterns as noticed during the fleet; promote to build when instances hit ≥3)*

### Rejected — not shippable as a precise rule
*(patterns that recurred but couldn't be made low-noise; this record proves selectivity)*
