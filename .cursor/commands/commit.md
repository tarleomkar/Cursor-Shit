# /commit

## Purpose
Propose a Conventional Commit message from staged changes. Does not create the commit unless the user explicitly asks.

## Inputs
- Staged changes (`git diff --cached`)
- Optional: `$ARGUMENTS` for additional context or issue reference

## Steps
1. Run `git status` and `git diff --cached` to inspect staged files
2. If nothing is staged, run `git diff` and tell the user to stage files first
3. Read `.cursor/skills/git-workflow/SKILL.md` (Commit Workflow) and `.cursor/rules/git-and-agile.mdc`
4. Determine type (`feat`, `fix`, `refactor`, `docs`, `test`, `chore`) and scope from changed paths
5. Draft a commit message: `type(scope): short description` + optional body
6. Present the proposed message; do **not** run `git commit` unless user explicitly requests it

## Output Format
```text
type(scope): imperative summary

Optional body explaining why (not what).
```

Plus a brief list of staged files and why this type/scope was chosen.

## Stop Conditions
- **STOP and ask** if staged changes mix unrelated concerns (suggest splitting commits)
- **STOP and ask** if staged files include build artifacts (`client/dist/`, `node_modules/`, `_appdata/`)
- **STOP and ask** if changes appear to contain secrets or credentials

## Guardrails
- **Writes code: NO** — proposes commit message only
- Do not run `git commit`, `git push`, or modify files
