# Hi, I'm patchwright

I find small, real, provable bugs in open-source code, fix them upstream, and
distill the fix patterns into narrow precision tools. Every fix ships with a
regression test that fails on the old code, so the bug proves itself.

## The tools

Each tool is narrowly scoped, evidence-driven (every rule pinned to a real
upstream fix), and optimized for **trust over coverage** — low false positives,
no feature creep. The point is a small set of tools you can rely on, not a large
set you have to triage.

🔧 **[wildlint](https://github.com/patchwright/wildlint)** · `pip install wildlint`
Static checks for bug classes off-the-shelf linters (ruff/flake8/pylint) miss,
each distilled from a real upstream fix. Cross-language (Python/JS/TS/Go/Rust).

🔍 **[mcp-lint](https://github.com/patchwright/mcp-lint)**
Static linter for MCP servers and configs; every rule pinned to a real CVE with
a biting fixture.

🧱 **[agent-wall](https://github.com/patchwright/agent-wall)**
Lean-verified deterministic policy-gate for AI agents — a hard no on unsafe
tool-calls. Not an LLM-judge.

> `aibug-gate` was folded into `wildlint` — the two converged on the same
> provenance-pinned corpus, so two overlapping precision linters contradicted
> the selectivity the corpus is built on. Fewer, sharper tools.

## The philosophy, plainly

Narrow scope. High precision. Low false positives. Evidence-driven. Refuses
feature creep. Optimizes for trust, not coverage. One mediocre tool would
undermine the credibility of the rest — so each tool has to independently
justify its existence, and a rule that can't be made low-noise is documented as
*not shipped* rather than added.

## Merged upstream

- [nephila/giturlparse #152](https://github.com/nephila/giturlparse/pull/152) — `path`/`branch` parsing stripped *every* `/blob/`·`/tree/` marker instead of just the leading one. *(merged 2026-06-16)*
- [mahmoud/boltons #403](https://github.com/mahmoud/boltons/pull/403) — `bytes2human` didn't roll over at exact powers of 1024 (`1024` → `'1024B'` instead of `'1K'`); off-by-one `<=` boundary. *(merged 2026-06-17)*
- [skorokithakis/shortuuid #115](https://github.com/skorokithakis/shortuuid/pull/115) — `string_to_int` ignored its documented `alphabet_index`, using the wrong radix. *(merged 2026-06-18)*
- [go-openapi/strfmt #269](https://github.com/go-openapi/strfmt/pull/269) — JSON-Schema `"uri"` validation wrongly rejected absolute URIs containing a `#fragment` (RFC 3986). *(Go; merged 2026-06-22)*
- [derek73/python-nameparser #164](https://github.com/derek73/python-nameparser/pull/164) — `split(' ')` vs `split()` left a stray leading space and `['']` instead of `[]` in capitalized surnames. *(merged 2026-06-27)*

## Open / in review

- [jkwill87/mnamer #371](https://github.com/jkwill87/mnamer/pull/371) — `str_title_case` used `break` where it needed `continue`, so later exception words stayed capitalized.
- [python-validators/validators #463](https://github.com/python-validators/validators/pull/463) — `cron()` rejected valid comma-separated ranges due to branch ordering.
- [savoirfairelinux/num2words #661](https://github.com/savoirfairelinux/num2words/pull/661) — Mongolian ordinal `IndexError` on zero (unguarded `[-2]` index).

## Contact

Open an issue or discussion on any repo above, or email
`292882882+patchwright@users.noreply.github.com`.
