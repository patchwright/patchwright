# patchwright

**Making experiment findings survive.**

Most experiment findings die — not wrong, dead. They're faked (verdict ungrounded,
collapses under load) or orphaned (correct but reaches no decision, leaks into
nothing). Tracking tools (MLflow, W&B, DVC) cover metrics and params; none covers
the verdict layer — *what was actually established*. So the finding leaks.

This is the work of making knowledge survive: findings that are **true-checkable**
(verdict grounded in evidence you can point at) **and connected-queryable** (stable
identity + verdict a downstream can act on). Both, or it dies.

## The lead

- **[finding-declaration](https://github.com/patchwright/finding-declaration)** — a machine-readable standard for declaring experiment findings. 5 required fields, a 5-state verdict vocabulary derived across 8 experimental domains. Verified uncovered across 40+ tracking tools and metadata standards. Dogfooded on 170 real findings.
- **[findcheck](https://pypi.org/project/findcheck/)** — the reference validator. `pip install findcheck`.
- *Most of your experiment findings are already dead* — [the first piece](https://github.com/patchwright/finding-declaration/blob/main/content/01-findings-are-dying.md) on why knowledge leaks and what stops it.

## The test this publisher holds to

Every artifact under patchwright answers one question: **does this make signal more
true-checkable, or more connected-queryable?** If neither, it's off-thesis and won't
be foregrounded here. The principle is testable — you can check it per artifact, and
so can anyone else.

## Note on the rest of the repo list

The list also contains earlier tools (wildlint, mcp-lint, agent-wall, schemasmoke,
mutaprobe) and a number of upstream fix-PR forks. They're maintained or archived as
they stand, but they are **not** the focus — the surface narrowed to findings-integrity
in 2026-07. The reason is straightforward: scattered work across unrelated domains
does not compound into trust, and a narrowed, consistent catalog does. The earlier
work isn't repackaged as something it wasn't; it's just no longer what this publisher
points at.

---

*Knowledge doesn't survive because you're careful. It survives because you encoded
it to survive.*
