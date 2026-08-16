# openspec-base — Context & Handoff

## What This Repo Is

A starter template for bootstrapping new projects with the **OpenSpec spec-driven development workflow** already wired in. Clone it to get the full artifact lifecycle (planning → design → implementation → verification → archival) pre-configured for OpenCode, GitHub Copilot, and Claude Code.

## Core Concept

Every change (feature, fix, refactor) follows a deterministic artifact sequence before any code is written:

```
proposal.md → specs/<capability>/spec.md → design.md → [adr/*.md] → tasks.md
```

Changes live in isolated directories under `openspec/changes/<change-name>/`. On completion, delta specs are merged into `openspec/specs/` (the living system documentation) and the change is archived.

## Key Artifacts

| File | Purpose |
|------|---------|
| `proposal.md` | Problem statement, scope, capabilities affected |
| `specs/<cap>/spec.md` | Delta specification for a specific capability |
| `design.md` | API contracts, DB schema, system boundaries |
| `docs/adr/*.md` | Architecture Decision Records |
| `tasks.md` | Atomic, granular implementation tasks with `TaskID` and `Verify` commands |
| `qa_report.md` | Test results and verification evidence |
| `implementation_notes.md` | Decisions made during coding |
| `draft_pr.md` | PR description generated after implementation |

## Slash Commands (Available in OpenCode, GitHub Copilot & Claude Code)

| Command | What It Does |
|---------|-------------|
| `/opsx-new <change>` | Start a new change, step-by-step |
| `/opsx-propose <change>` | Fast-path: generate all artifacts in one shot |
| `/opsx-continue` | Advance to the next artifact in the sequence |
| `/opsx-apply <change>` | Execute tasks from `tasks.md` |
| `/opsx-verify <change>` | Confirm completeness, correctness, coherence |
| `/opsx-sync <change>` | Merge delta specs into `openspec/specs/` |
| `/opsx-archive <change>` | Move completed change to `openspec/changes/archive/` |
| `/opsx-explore` | Thinking-partner mode before starting a change |

Skills live in `.opencode/skills/` (OpenCode), `.github/skills/` (GitHub Copilot), and `.claude/skills/` (Claude Code). Commands mirror each other across all three surfaces.

## Repository Structure

```
openspec/
  config.yaml              # Workflow schema declaration + project context
  specs/                   # Main system specifications (living docs)
  schemas/
    spec-driven-with-adr/  # Schema definition + artifact templates
changes/
  <change-name>/           # Active change directory
    .archived              # Sentinel file when archived
    proposal.md
    design.md
    tasks.md
    ...
docs/adr/                  # Architecture Decision Records
.opencode/commands/        # opsx-* OpenCode slash commands
.opencode/skills/          # openspec-* skills (implementation of commands)
.github/prompts/           # Mirrors .opencode/commands/ for GitHub Copilot
.github/skills/            # Mirrors .opencode/skills/ for GitHub Copilot
.claude/commands/          # Mirrors .opencode/commands/ for Claude Code
.claude/skills/            # Mirrors .opencode/skills/ for Claude Code
.agents/skills/            # Extra skills: c4-diagrams, grill-me, grill-with-docs
AGENTS.md                  # Repo structure overview for agents
```

## Current State

- Schema: `spec-driven-with-adr` (see `openspec/config.yaml`)
- Context field in `config.yaml` is intentionally blank — fill it per project
- Three sample changes in `changes/`: `smoke-local` (archived), `llm-smoke` (archived), `smoke-cloud` (in progress)

## Relationship to agentic-sdlc-engine

`agentic-sdlc-engine` uses `openspec-base` as the artifact template source. The engine's `FilesystemAdapter` reads schemas and writes change directories following this repo's conventions. Changes created by the engine are fully compatible with the manual `/opsx-*` commands.
