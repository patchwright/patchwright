# Hi, I'm patchwright

I find real bugs in open-source code and fix them. Every fix ships with a regression test that fails on the old code, so the bug proves itself.

## Pull requests
- [nephila/giturlparse #149](https://github.com/nephila/giturlparse/pull/149) — `path`/`branch` parsing stripped every `/blob/`/`/tree/` marker instead of just the leading one.
- [jkwill87/mnamer #371](https://github.com/jkwill87/mnamer/pull/371) — `str_title_case` used `break` where it needed `continue`, so later exception words stayed capitalized.
- [python-humanize/humanize #326](https://github.com/python-humanize/humanize/pull/326) — `fractional()` doubled the minus sign on negative mixed numbers.

## Tooling
- [replace-prefix-lint](https://github.com/patchwright/replace-prefix-lint) — zero-dep AST linter for the `.replace(prefix,"")` pattern that ruff B005 misses.

## Contact
Open an issue on any repo above, or email `292882882+patchwright@users.noreply.github.com`.