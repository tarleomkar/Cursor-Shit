# /implement

## Purpose
Execute an **approved plan** using the `feature-development` skill. Implement task-by-task in small commits.

## Inputs
- Approved Plan.md checklist from a prior `/plan-feature` run (or pasted in chat)
- Optional: `$ARGUMENTS` to specify which task(s) to execute

## Steps
1. Read `.cursor/skills/feature-development/SKILL.md` and follow workflow **steps 6–8**
2. Confirm the plan exists and is approved; if not, tell the user to run `/plan-feature` first
3. Work through tasks **one at a time** in plan order; mark each complete in the checklist
4. Only touch files listed in the plan's Impact Analysis (or ask before adding new files)
5. Follow `.cursor/rules/architecture.mdc`, `coding-standards.mdc`, `design-patterns.mdc`, `security-baseline.mdc`
6. Add tests per `.cursor/rules/testing-standards.mdc` for each behavior change
7. After all tasks: run `cd server && npm test` if server files changed
8. After all tasks: run `cd client && npm run lint` if client files changed
9. Self-check Definition of Done from `git-and-agile.mdc`; report results

## Files You May Touch
Only files explicitly listed in the approved plan's Impact Analysis, plus their corresponding test files under `server/test/`. Do not edit `node_modules/`, `client/dist/`, `server/_appdata/`, or `server/_pkg/`.

## Output Format
Updated Plan.md checklist with completed tasks checked, plus a summary:
- Files changed
- Tests added
- `npm test` / `npm run lint` results
- Remaining DoD items (if any)

## Stop Conditions
- **STOP and ask** if no approved plan exists in the conversation
- **STOP and ask** if a task requires touching files outside the impact analysis
- **STOP and ask** if tests fail and the fix scope exceeds the current task
- **STOP and ask** if a new npm dependency would be required

## Guardrails
- **Writes code: YES** — only approved-plan files + tests
- MUST run tests/linters after implementation per steps 7–8
