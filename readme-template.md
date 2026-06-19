# <Project Name>

> **Per-project, fill-in stub** (like the PRD — `prd-template.md`). Part of the **Kickoff
> Kit** (see `claude-project-kickoff.md`). This is the project's **human front door**: for a
> capable reader who may not be a software engineer — what it is, how to run it, how to use
> it. It is **not** the agent contract (`CLAUDE.md`) or the deep docs (the wiki); keep those
> concerns out of here. Write in plain language, lead with the reader's outcome, keep it
> short. Delete this note and the `<…>` prompts as you fill it in.

<One sentence anyone can follow: what this is and who it's for. Lead with the outcome, not
the tech — e.g. "A private dashboard that pulls your fitness-ring data onto hardware you own
and shows your sleep, readiness, and risk trends.">

<!-- reconcile-code: PUT-PATHS-HERE -->
<!-- ^ Keep the line above on ONE line. List the files whose change would make this README
     wrong: the run/CLI entry point(s), the dependency manifest, the main API/router, the
     config loader. The audit (kickoff §1.6) and the wiki reconcile pass use it to flag this
     README as stale when those files move ahead of it. Update the README in the SAME commit
     as the code it describes and the staleness check stays quiet. Keep the list short + real. -->

## What it does
<2–4 plain sentences or bullets: the job it does and why it's useful. Outcomes, not
architecture. If a screenshot says it faster, put one here.>

## Quick start
<The shortest path from nothing to running, copy-pasteable. Prereqs (runtime + version),
install, configure, run — the happy path only.>

```sh
<install>      # the one install command
<configure>    # copy the example env, set the required vars — NEVER paste a real secret here
<run>          # the one command that starts it
```

## Using it
<The 2–4 things a person actually does once it's running — the main features or workflows,
in plain terms. This is the section a non-engineer cares about most.>

## Configuration
<The settings / environment variables a user can or must set, what each does, and safe
defaults. Say where secrets live (an untracked `.env`, a secret store) — never inline a real
value (a tracked secret is an audit failure).>

## Status
<ONE honest, coarse line — e.g. "Working: sync + dashboard. In progress: alerts." Do NOT
keep a detailed per-feature checklist here: a hand-maintained status list rots fastest of
all and ends up lying about what's built. For finer detail point to the issue tracker or the
PRD, and let the test suite + git history be the real record of what exists.>

## How it's built (the short version)
<One paragraph for the curious reader: the rough shape — e.g. "a sync job → a local database
→ a read-only API → a web dashboard." Then point deeper instead of duplicating: the build
contract and invariants live in `CLAUDE.md`, the subsystem depth and decision history in the
wiki, the requirements in the PRD.>

## Project map
<A few lines: where the entry points and main directories are, so a newcomer can find their
way. One line per top-level area, not a full tour.>
