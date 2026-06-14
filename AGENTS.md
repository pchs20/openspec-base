# AGENTS.md

## Repo structure

```
openspec/          # OpenSpec artifact workflow config
  config.yaml      # schema: spec-driven (context field still empty — fill me)
  specs/           # main specs (empty — create via /opsx-new)
  changes/         # active change directories
    archive/       # archived/complete changes
.opencode/         # OpenCode config
  skills/          # openspec-* skills installed
  commands/        # opsx-* slash commands (opsx-new, opsx-propose, opsx-apply, etc.)
.github/           # GitHub config
  prompts/         # GitHub PR comments prompts (mirrors .opencode/commands/)
  skills/          # GitHub Actions skills (mirrors .opencode/skills/)
```
