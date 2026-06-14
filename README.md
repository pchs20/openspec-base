# OpenSpec Base Repository

## Idea

This repository is a personal starter base for creating new projects with OpenSpec already wired in.

The goal is to avoid repeating setup work each time I start something new. Instead of bootstrapping OpenSpec from scratch per project, I can clone/copy this base and immediately start proposing and implementing changes using the OpenSpec workflow.

## What this base already includes

- Core OpenSpec structure under `openspec/`
	- `openspec/config.yaml`
	- `openspec/specs/`
	- `openspec/changes/archive/`
- OpenCode integration under `.opencode/`
	- `commands/` with `opsx-*` command docs
	- `skills/` with `openspec-*` skills
	- plugin dependency (`@opencode-ai/plugin`) in `.opencode/package.json`
- GitHub Copilot integration under `.github/`
	- `prompts/` mirroring opsx commands
	- `skills/` mirroring openspec skills
- A project-level `AGENTS.md` describing structure and intent.

## Reconstructed process used to get here

Based on repository contents, this is the most likely sequence that was executed:

1. Initialized OpenSpec in the repo.
2. Configured OpenSpec profile for OpenCode.
3. Configured OpenSpec profile for GitHub Copilot.
4. Added `AGENTS.md` manually as local documentation.

## Working baseline for future projects

When starting a new project from this base:

1. Copy/clone this repository into the new project location.
2. Customize `openspec/config.yaml` context section for the project's tech stack and conventions.
3. Start the first change with the opsx workflow (`new`, then `continue`, then `apply`, etc.).

This base is intentionally minimal: it sets up the OpenSpec workflow scaffolding and assistant integrations, while leaving specs and changes empty for each new project.

## Expected way to work with OpenSpec (plan -> build -> close)

This is the expected operating loop when using this base.

### 1) Explore and clarify

- Use `/opsx-explore` to think through ideas, constraints, and tradeoffs before creating artifacts.
- This mode is for discovery and problem framing, not implementation.

### 2) Start planning a change

Choose one planning style:

- Guided, step-by-step artifact creation:
	- `/opsx-new <change-name>`
	- then repeatedly `/opsx-continue <change-name>` to create the next artifact in order
- Fast, one-shot proposal flow:
	- `/opsx-propose <change-name>` to create change + planning artifacts in one go

In spec-driven workflows, artifacts usually progress like:

1. `proposal.md`
2. `specs/<capability>/spec.md` (one per capability)
3. `design.md`
4. `docs/adr/*.md` (when the design introduces durable architectural decisions)
5. `tasks.md`

### 3) Implement from tasks

- Run `/opsx-apply <change-name>`.
- Implement tasks incrementally and keep `tasks.md` checkboxes updated (`[ ]` -> `[x]`).
- If implementation reveals design/spec gaps, update artifacts and continue.

### 4) Verify before closing

- Run `/opsx-verify <change-name>`.
- Verify focuses on:
	- completeness (tasks/requirements covered)
	- correctness (implementation aligns with requirements/scenarios)
	- coherence (implementation matches design intent)

### 5) Sync delta specs into main specs

- Run `/opsx-sync <change-name>`.
- This merges change delta specs into `openspec/specs/...` so main specs stay current.

### 6) Archive completed change

- Run `/opsx-archive <change-name>`.
- This moves the completed change into `openspec/changes/archive/YYYY-MM-DD-<change-name>/`.

## Practical command map

- Explore: `/opsx-explore`
- New change (guided): `/opsx-new <name>`
- Continue artifact flow: `/opsx-continue <name>`
- Propose in one pass: `/opsx-propose <name>`
- Implement tasks: `/opsx-apply <name>`
- Verify implementation: `/opsx-verify <name>`
- Sync specs: `/opsx-sync <name>`
- Archive: `/opsx-archive <name>`

## Suggested working rhythm

1. Explore quickly if needed.
2. Plan artifacts until tasks are clear.
3. Implement via `/opsx-apply` and keep tasks updated.
4. Verify with `/opsx-verify`.
5. Sync specs with `/opsx-sync`.
6. Archive with `/opsx-archive`.
