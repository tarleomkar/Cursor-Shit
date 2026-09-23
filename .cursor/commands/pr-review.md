# /pr-review

## Purpose
Review the current branch changes against `main` using the `pr-review` skill.

## Inputs
- Current git branch diff vs `origin/main` (fallback: `main`, `master`)
- Optional: `$ARGUMENTS` for PR description or focus area (security, performance, etc.)

## Steps
1. Run `git diff origin/main...HEAD` and `git log origin/main..HEAD --oneline` to gather changes
2. If `origin/main` is unavailable, try `main`, then `master`; ask the user if all fail
3. Read `.cursor/skills/pr-review/SKILL.md` and follow its full workflow
4. Review diff for correctness, tests, security, readability, performance, backward compatibility, docs
5. Check against `.cursor/rules/` and `.github/pull_request_template.md`
6. Produce findings as Blockers, Suggestions, Nitpicks with `file:line` refs
7. Give a verdict: **Approve** or **Request changes**

## Output Format
PR Review: Summary, Blockers, Suggestions, Nitpicks, Checklist, Verdict.

## Stop Conditions
- **STOP and ask** if there is no diff vs base branch (nothing to review)
- **STOP and ask** if base branch name is ambiguous

## Guardrails
- **Writes code: NO** — review report only
- Do not modify source files or create commits
