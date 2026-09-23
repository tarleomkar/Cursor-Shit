# FUXA Agent Guide

Cursor config lives in `.cursor/` — see [.cursor/README.md](.cursor/README.md) for the full map.

**Agile flow:** Story → `/plan-feature` → `/implement` → `/test-feature` → `/pr-review` → `/dod-check` → merge

**Rules** (`.cursor/rules/*.mdc`) enforce constraints. **Skills** (`.cursor/skills/*/SKILL.md`) define workflows. **Commands** (`.cursor/commands/*.md`) invoke skills. **Subagents** (`.cursor/agents/*.md`) handle read-only review and test verification.

**Priority when instructions conflict:** safety rules → repo rules (`.cursor/rules/`) → skill instructions → ad-hoc prompts

**Base branch for diffs:** `origin/main` (fallback: `main`, then `master`).
