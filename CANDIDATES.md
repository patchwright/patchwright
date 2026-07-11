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
AB007 + AB008 are **resolved** — already covered by wildlint's WP001 rollover property
test (not ported; static ports refused — see entries). Three remain to migrate
(AB002, AB005, AB006), each ~1 instance → `pedantic` or needs-more-evidence.

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
- **log-derived exponent + rounded mantissa, no carry-guard** ("1000.0 kB") — ✅ RESOLVED (not ported).
  - Instance: python-humanize/humanize#329 (merged).
  - Verdict: **covered by wildlint WP001** (`find_rollover` property test — `humanize` is its default target; humanize#329 now cited). Static port REFUSED: wildlint uses the property test precisely because a static rule for this class flags mountains of correct code; porting the static version would reintroduce that noise.
- **magnitude-binning loop breaks on `<=` at boundary** (1024 → "1024B") — ✅ RESOLVED (not ported).
  - Instance: mahmoud/boltons#403 (merged).
  - Verdict: **already covered by wildlint WP001** (boltons#403 was already a cited instance). Static port refused, same reason.

### Needs more evidence
*(add patterns as noticed during the fleet; promote to build when instances hit ≥3)*

### Rejected — not shippable as a precise rule
*(patterns that recurred but couldn't be made low-noise; this record proves selectivity)*
