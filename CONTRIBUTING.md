# Contributing

This list covers four parts of agent reliability: **Loops**, **Multi-Agent / Graph Orchestration**, **Security**, and **Rust** for building agents.

- One entry per PR, in the right part and section, alphabetical within its section where practical.
- Format: `[name](url) - What it is and why it matters for that part (one line).`
- Scope, by part:
  - **Loops** — patterns, runners, and write-ups for single agents running in autonomous, self-feeding cycles.
  - **Multi-Agent / Graph Orchestration** — topology patterns, frameworks, protocols, state/durability, observability, and evals for systems with more than one agent or node.
  - **Security** — skills/plugins/MCP/hooks/runtime/red-teaming for autonomous agents. Generic infosec or generic ML belongs elsewhere.
  - **Rust** — Rust crates/tools (or projects with a first-class Rust interface) for building agents. No unmaintained or archived projects.
- Each entry goes in one place only — if it fits several sections, pick the best one rather than duplicating it.
- No dead links, no vendor marketing pages without substance, no self-promotion sections.
- Cite papers by their real authors and arXiv IDs — check the link resolves to the paper you describe.
- New sections need 3+ entries to justify themselves.
- Every PR runs the link checker (`.github/workflows/link-check.yml`, configured in `lychee.toml`). If a live link fails only because its host blocks CI, add a narrowly-scoped `exclude` entry with a comment saying when you verified it by hand.
