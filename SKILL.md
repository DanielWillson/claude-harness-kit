---
name: project-kickoff
description: >
  Set up a brand-new project the Kickoff Kit way: machine + repo safety floor, tailored
  settings, a CLAUDE.md contract, a health-check audit, a knowledge wiki, a human README,
  and the building principles. Use when the user is starting a new project from scratch,
  asks to "run the kickoff" / "kick off this project", or wants a project setup ritual.
  NOT for ongoing work in a project that is already set up.
---

# Project Kickoff (the Kickoff Kit, as a skill)

This skill packages the **Claude Kickoff Kit** — a portable, stack-agnostic setup ritual
plus building philosophy for brand-new projects. The kit's documents live in this same
directory. Drive the ritual **from the kickoff guide**; read companions only when a step
calls for them.

## How to run it

1. Read `claude-project-kickoff.md` — the driver. It contains the one-time machine
   hardening (Part 0), the per-project setup ritual with its nine-question intake
   (Part 1), the building principles (Part 2), and the autonomous/multi-agent playbook
   (Part 3).
2. Execute Part 1 for *this* project, adapting every example to the user's actual stack —
   the guide is explicit that every concrete tool it names is an example, not an
   assumption.
3. Pull companions when their step comes up, not before:
   - `llm-wiki-kickoff.md` → §1.5b, before scaffolding the wiki (Standard tier and up)
   - `claude-audit-base.sh` → §1.6, copy to `scripts/audit.sh`, wire the TOOLING section
   - `readme-template.md` → §1.5c, the human-facing README
   - `prd-template.md` → §1.7, hand to the user to fill in if no spec exists
   - `templates/` + `CHEATSHEET.md` → Part 0 / §1.3, the settings layers
   - `securing-claude-sessions.md` → only if the user wants the security model explained
4. Confirm setup, remind the user to enter auto mode and restart so the sandbox
   initializes (§1.7), then ask for the spec.

## Boundaries (the kit's own)

- The kit is scaffolding, used once. **Never copy its files into the project repo**, and
  never `@`-import them from the project's `CLAUDE.md`. Only the ritual's *outputs*
  persist: `CLAUDE.md`, `.claude/settings.json`, `scripts/audit.sh`, `wiki/`, `README.md`,
  the filled-in PRD.
- This skill cannot install the machine-wide managed floor (it is root-owned by design) —
  walk the user through Part 0 by hand instead.
- If the project already exists and is set up, this skill does not apply: work from the
  project's own `CLAUDE.md` and wiki, not the kit.
