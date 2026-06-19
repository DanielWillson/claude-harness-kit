# Claude Kickoff Kit

A portable set of docs you hand to a fresh Claude Code session **at the start of a new
project** — a setup ritual, a working philosophy, and the templates that seed a project's
durable knowledge, health checks, and docs. It is *project-agnostic scaffolding*: used once
per project, and **never committed into the project's own repo**.

## What's in here
- **`claude-project-kickoff.md`** — the entry point. The setup ritual (git, a sandboxed
  `.claude/settings.json`, `CLAUDE.md`, the audit, the wiki), the building principles, and the
  autonomous / multi-agent playbook. Read this first; it drives the rest.
- **`llm-wiki-kickoff.md`** — how to stand up the project's self-maintaining,
  reconcile-against-code knowledge **wiki** (the depth + decision/incident-history layer).
- **`claude-audit-base.sh`** — a stack-agnostic code-health **audit** you copy to
  `scripts/audit.sh` and grow with each invariant and every fixed bug.
- **`prd-template.md`** — a fill-in PRD/spec skeleton (what & why, invariants, open decisions).
- **`readme-template.md`** — a fill-in, **human-facing** project README stub (the project's
  front door), with a `reconcile-code` anchor so the audit flags it when it drifts from the code.
- **`styleguide.html`** — an *example* per-project design styleguide (swap in your own).

## How to use it
At a new project's kickoff, hand Claude the relevant files (always the kickoff guide; the
others as the project needs them). Claude runs the setup, internalizes the principles, and
produces the project's **durable artifacts** — `CLAUDE.md`, `.claude/settings.json`,
`scripts/audit.sh`, `wiki/`, `README.md`, and the filled-in PRD. *Those* live in the project
repo; this kit does not. After buildout the kit drops away — ongoing work reads the project's
lean `CLAUDE.md` + wiki, never this kit.

## Design stance
- **Self-improving knowledge** — the wiki (and the project README) reconcile against the
  code, so docs can't silently rot.
- **Lean on the repo, not machine-local memory** — project knowledge lives in the repo (wiki
  + `CLAUDE.md` + commit bodies); machine-local memory is for user-level preferences only.
- **Scaffolding vs. artifacts** — the kit is used once; only its outputs persist (the audit
  even warns if a kit source file gets committed into a project).

> The styleguide and PRD are interchangeable per project; the guides and templates are the
> reusable core.
