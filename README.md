# Claude Kickoff Kit

A portable set of docs you hand to a fresh Claude Code session **at the start of a new
project** — a setup ritual, a working philosophy, and the templates that seed a project's
durable knowledge, health checks, and docs. It is *project-agnostic scaffolding*: used once
per project, and **never committed into the project's own repo**.

## The idea: you build the harness, not the prompt

A framing from the emerging practice around coding agents puts it cleanly: **Agent = Model +
Harness** (Fowler). The model is fixed; what you actually shape is everything around it — the contract it reads,
the checks it must pass, the boundaries it can't cross, the knowledge it can recall. That
surrounding structure, far more than any single prompt, decides whether an agent does reliable
work.

Two senses of "harness" sit close together, and the kit keeps them apart on purpose:
- the **runtime** harness — Claude Code itself (the agent loop, the tools, the auto
  classifier). You don't build this; you configure it.
- the **durable** harness — the repo-resident scaffolding the kit produces: `CLAUDE.md`,
  `.claude/settings.json`, `scripts/audit.sh`, `wiki/`, `README.md`, the filled-in PRD. This
  is what the kit is *for*, and it outlives any one session or model upgrade.

The kit's job is to stand up that durable harness in one sitting and then get out of the way.

## How the pieces fit together

Borrowing Fowler's vocabulary, the durable harness is a system of two kinds of control, each
aimed at raising confidence in what the agent produces:

- **Guides (feedforward)** steer the agent *before* it acts: `CLAUDE.md` (the always-loaded
  contract), the PRD/spec, the styleguide and its design tokens, the load-bearing audit
  *invariants*, and — at fan-out time — the frozen `CONTRACT.md` snapshot. These raise the
  odds of a correct first draft.
- **Sensors (feedback)** observe *after* it acts and let it self-correct: `scripts/audit.sh`
  (deterministic greps + regression guards), the test suite and a machine-checkable Definition
  of Done, adversarial plan/code review, the audience-persona panel, and the wiki's
  reconcile-against-code pass. These catch what the guides missed.

The loop closes by hand. When a sensor catches a recurring miss, you *strengthen a guide*: the
bug becomes a permanent regression guard in the audit, the surprise becomes a one-line
guardrail in `CLAUDE.md`, the dead end becomes a wiki incident page. That ratchet — every fixed
mistake leaves behind something that stops it returning — is the single highest-leverage habit
the kit installs. It is also why the docs are built to **reconcile against the code** instead of
being trusted on faith: a guide or a knowledge page that can silently go stale is worse than
none, because the agent will act on it with full confidence.

**Security is a separate axis — don't fold it into "guides and sensors."** The distinction the
kit guards most carefully is that controls differ in *kind*:

> the OS sandbox is the **boundary**; `deny`/`ask` rules are **deterministic backstops**; the
> auto classifier is a **probabilistic backstop**; `CLAUDE.md` / `autoMode` prose is **not a
> control** at all.

So `deny`/`ask` are *not* "guides" in Fowler's advisory sense — they don't steer, they bind, at
action time, in every mode. Treating a hard rule as if it were soft prose (or the reverse) is
the exact mistake the security model exists to prevent. `securing-claude-sessions.md` and
`CHEATSHEET.md` carry this axis in full; the quality harness above rides on top of it.

## What's in here

Each entry notes what it *is* in the harness, and why it earns its place.

- **`claude-project-kickoff.md`** — the entry point: the setup ritual (git, a sandboxed
  `.claude/settings.json`, `CLAUDE.md`, the audit, the wiki), the ten building principles, and
  the autonomous / multi-agent playbook. Read this first; it drives the rest. *(It defines most
  of the guides and sensors and how to wire them together.)*
- **`llm-wiki-kickoff.md`** — how to stand up the project's self-maintaining knowledge
  **wiki**: the depth + decision/incident-history layer, and the project's **"system of
  record."** Its load-bearing idea is *reconcile against ground truth, not against itself* — the
  code is the source of truth, so a stale page is detected rather than believed. *(A sensor for
  knowledge drift, and the home for the "we tried X, it failed because Y" history nothing else
  captures.)*
- **`claude-audit-base.sh`** — a stack-agnostic code-health **audit** you copy to
  `scripts/audit.sh` and grow with each invariant and every fixed bug. *(The kit's primary
  deterministic sensor: fast, CPU-only, runs anywhere — and where the ratchet lives.)*
- **`prd-template.md`** — a fill-in PRD/spec skeleton (what & why, invariants, open decisions).
  *(A guide: where the load-bearing invariants get named before any code exists, then graduate
  into audit checks.)*
- **`readme-template.md`** — a fill-in, **human-facing** project README stub (the project's
  front door), with a `reconcile-code` anchor so the audit flags it when it drifts from the
  code. *(Distinct from `CLAUDE.md`: humans read this, the agent reads the contract — keeping
  the audiences apart is deliberate, see below.)*
- **`styleguide.html`** — an *example* per-project design styleguide (swap in your own). *(A
  guide for the UI layer; its tokens become the one source of truth components reference.)*
- **`templates/`** — copy-paste **settings templates**: `managed-settings.template.json` (the
  machine-wide hard floor), `project.settings.json` (the committed per-repo floor), and
  `project.settings.local.json.example` (per-machine sandbox-enable + `autoMode`). See
  `templates/README.md` for the three-layer model. *(The security axis — the boundary and the
  deterministic backstops — not the quality harness.)*
- **`CHEATSHEET.md`** — the verified Claude Code permission/sandbox mechanics (Bash-only
  sandbox, deny-rules-are-a-sieve, settings precedence + array-merge, launch-dir-only load,
  macOS egress limits).
- **`securing-claude-sessions.md`** — a narrative **field guide** to the security model (the
  five enforcement levels, defense-in-depth, *"a control is only as strong as the agent's
  inability to reach it"*). The teaching companion to `CHEATSHEET.md`; written against an
  example deployment.

## How to use it

At a new project's kickoff, hand Claude the relevant files (always the kickoff guide; the
others as the project needs them). Claude runs the setup, internalizes the principles, and
produces the project's **durable artifacts** — `CLAUDE.md`, `.claude/settings.json`,
`scripts/audit.sh`, `wiki/`, `README.md`, and the filled-in PRD. *Those* live in the project
repo; this kit does not. After buildout the kit drops away — ongoing work reads the project's
lean `CLAUDE.md` + wiki, never this kit.

The autonomy posture this enables is, in the field's words, **"humans steer, agents execute"**
(OpenAI) — read precisely. *Steering* means setting the deterministic `deny`/`ask` gates and
reviewing small commits after the fact; it does **not** mean approving each step (that fights
autonomy) or stating a boundary in chat (which is lost when context compacts). *Execution* is
hands-off auto mode plus adversarial-*agent* review.

## Design stance

- **Self-improving knowledge** — the wiki (and the project README) reconcile against the code,
  so docs can't silently rot. A knowledge base trusted on faith decays into confident lies; one
  checked against ground truth decays *visibly*, which is the only kind of decay you can act on.
  It's the knowledge analogue of *"keep quality left"* (Fowler): catch drift continuously and
  cheaply, rather than discovering it the moment an agent builds on a stale page.
- **Lean on the repo, not machine-local memory** — project knowledge lives in the repo (wiki +
  `CLAUDE.md` + commit bodies); memory is for user-level preferences only, and a
  project-specific fact never goes in global `~/.claude/CLAUDE.md` (it would pollute every other
  project). Default any project fact to the wiki. The governing line, in the field's words:
  *"anything [the agent] cannot access in context at runtime does not exist"* (OpenAI) — so the
  contract is a lean **table of contents**, not an encyclopedia, with the depth one pointer
  away.
- **Three audiences, three docs, no overlap** — the human `README` (front door), the agent
  `CLAUDE.md` (always-loaded invariants + pointers), and the wiki (on-demand depth + history).
  Most agent setups collapse the first two; keeping them apart is what lets the contract stay
  lean *and* the human doc stay readable, each reconciled against the code its own way.
- **Tool-agnostic by the repo, not by one agent** — the durable rules live where *any* tool
  reads or runs them: the contract's *content* (read by any LLM/tool/human) and the audit (run
  on demand or in CI). Claude-specific machinery (the Stop-hook auto-commit,
  `.claude/settings.json`, `/wiki`) is a convenience *adapter* on top. When a second committer
  is in play (another LLM, a teammate, CI), a coarse secret-only `git` pre-commit hook + the
  audit-in-CI carry the guarantee (kickoff §1.3b). Auto-commit itself can't be made
  tool-agnostic — git has no commit-on-change event — so only the *rules* travel, not the *act*
  of committing.
- **Scaffolding vs. artifacts** — the kit is used once; only its outputs persist (the audit
  even warns if a kit source file gets committed into a project).
- **The hard floor is machine-level, not repo-level** — the un-negotiable *security* floor
  (no-bypass, credential denies, the OS sandbox) lives in **root-owned managed settings + the OS
  sandbox** (kickoff **Part 0**), because a committed `.claude/settings.json` is agent-editable
  and therefore *soft*. The committed per-repo floor still carries project specifics and the
  gates that should travel to teammates; array-merge keeps both layers live at once. The model:
  *the sandbox is the boundary; `deny`/`ask` are deterministic backstops; the classifier is
  probabilistic; prose is not a control* (see `CHEATSHEET.md`).

> The styleguide and PRD are interchangeable per project; the guides and templates are the
> reusable core.
