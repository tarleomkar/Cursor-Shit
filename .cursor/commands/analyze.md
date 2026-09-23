# /analyze

## Purpose
Run read-only codebase analysis via the `code-analysis` skill on a scope provided by the user.

## Inputs
- `$ARGUMENTS`: file path, module name, or feature area (e.g. `server/api/jwt-helper.js`)
- If no arguments: use the currently selected file or open editor tab
- Optional depth: quick vs thorough (default: thorough)

## Steps
1. Read `.cursor/skills/code-analysis/SKILL.md` and follow its full workflow
2. Resolve scope from `$ARGUMENTS`, selection, or open file
3. Map entry points and dependencies for the scoped area
4. Identify complexity hotspots, duplication, dead code, and coupling violations
5. Rate every finding as Blocker / Major / Minor with `file:line` refs
6. Produce the report using the skill's Output Format

## Output Format
Code Analysis report: Summary, Entry Points table, Dependency Map, Findings (Blocker / Major / Minor tables with suggested fixes), approximate metrics.

## Stop Conditions
- **STOP and ask** if scope is empty and no file is selected or open
- **STOP and ask** if the scope is the entire repo (confirm depth and focus areas)

## Guardrails
- **Writes code: NO** — report only, never modify source files
- Do not run destructive or state-changing commands
