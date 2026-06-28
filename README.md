# Hi, I'm patchwright

I find small, real, provable bugs in open-source Python and fix them. Every fix
ships with a regression test that fails on the old code, so the bug proves
itself.

## Tooling

🔧 **[wildlint](https://github.com/patchwright/wildlint)** · `pip install wildlint`
Static checks distilled from real upstream bugs that off-the-shelf linters miss.
Each rule comes from an actual bug I found and fixed upstream — see the merges below.

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
