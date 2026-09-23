# /dod-check

## Purpose
Verify the Definition of Done from `git-and-agile.mdc` for the current branch. Report-only checklist audit.

## Inputs
- Current branch changes: `git diff origin/main...HEAD` (fallback: `main`, `master`)
- Optional: `$ARGUMENTS` to specify base branch

## Steps
1. Read `.cursor/skills/git-workflow/SKILL.md` (DoD Verification Workflow) and `.cursor/rules/git-and-agile.mdc`
2. Run `git diff origin/main...HEAD --stat` (fallback: `main`, then `master`) to identify changed areas
3. For each DoD item, verify status:
   - Code style: spot-check changed files against `coding-standards.mdc`
   - Server tests: run `cd server && npm test` if `server/` files changed
   - Client lint: run `cd client && npm run lint` if `client/` files changed
   - Auth tests: check if `server/test/authorization/` has new tests when auth changed
   - Docs: check if `docs/` updated when user-facing behavior changed
   - Build artifacts: verify no `client/dist/`, `node_modules/`, `_appdata/` in diff
   - Local testing: note if manual browser test is still needed
4. Produce a pass/fail checklist with evidence for each item

## Output Format
```markdown
# Definition of Done Check: <branch>

| # | DoD Item | Status | Evidence |
|---|----------|--------|----------|
| 1 | 4-space indent / style | ✅/❌ | ... |
...

## Summary
X/Y items passed. Blockers: ...
```

## Stop Conditions
- **STOP and ask** if base branch is ambiguous
- **STOP and ask** if the branch has no changes vs base

## Guardrails
- **Writes code: NO** — verification report only
- May run read-only checks (`npm test`, `npm run lint`, `git diff`); do not edit source files
