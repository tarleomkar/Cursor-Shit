---
name: pr-review
description: >-
  Reviews pull requests and local diffs for correctness, tests, security, readability,
  performance, backward compatibility, and docs. Use when the user asks for a PR
  review, code review, diff review, or merge readiness check.
---

# PR Review

## When to Use
- User asks to review a PR, branch diff, or uncommitted changes
- User asks "is this ready to merge?" or "review my changes"
- Post-implementation quality gate before opening a PR

## Inputs Needed
- Diff source: branch name, PR URL, or `git diff` output
- PR description or linked issue (if available)
- Intended change type: bug fix, feature, refactor, docs

## Project Rules (checklist source)
- `.cursor/rules/coding-standards.mdc` — style, naming, error handling
- `.cursor/rules/architecture.mdc` — layering violations
- `.cursor/rules/security-baseline.mdc` — auth, secrets, input validation
- `.cursor/rules/testing-standards.mdc` — test adequacy
- `.cursor/rules/git-and-agile.mdc` — PR hygiene, no build artifacts
- `.github/pull_request_template.md` — project PR checklist

## Workflow

1. **Read the diff** — `git diff`, `git log`, and changed file list
2. **Correctness** — logic bugs, edge cases, error paths, off-by-one, race conditions
3. **Tests** — new/changed behavior covered per `testing-standards.mdc`; auth tests in `server/test/authorization/`
4. **Security** — JWT checks, path traversal, secret exposure per `security-baseline.mdc`
5. **Readability** — naming, scope size, follows `coding-standards.mdc`
6. **Performance** — blocking I/O in hot paths, unbounded loops, large payload handling
7. **Backward compatibility** — API contract changes, config migration, device protocol impact
8. **Docs** — `docs/` updated when user-facing behavior changes
9. **PR hygiene** — no `client/dist/`, `node_modules/`, `_appdata/` per `git-and-agile.mdc`
10. **Verdict** — Approve or Request changes with prioritized findings

## Output Format

```markdown
# PR Review: <title or branch>

## Summary
<2-3 sentences on what changed and overall quality>

## Blockers
- [ ] `file:line` — <must-fix issue>

## Suggestions
- `file:line` — <should-fix improvement>

## Nitpicks
- `file:line` — <optional polish>

## Checklist
- [ ] Correctness
- [ ] Tests adequate
- [ ] Security (security-baseline.mdc)
- [ ] Architecture (architecture.mdc)
- [ ] Backward compatible
- [ ] Docs updated (if needed)
- [ ] No build artifacts

## Verdict
**Approve** | **Request changes**
<one-sentence justification>
```

## Done When
- Every Blocker cites `file:line` with a concrete fix
- All seven review dimensions are explicitly addressed
- Verdict is given with clear justification
- Review references project rules, not generic advice
