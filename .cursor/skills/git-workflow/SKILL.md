---
name: git-workflow
description: >-
  Handles Conventional Commits and Definition of Done verification for FUXA branches.
  Use when proposing commit messages, checking merge readiness, or auditing DoD compliance.
---

# Git Workflow

## When to Use
- User asks for a commit message or wants to verify merge readiness
- Branch is ready for PR and needs DoD audit
- `/commit` or `/dod-check` commands are invoked

## Inputs Needed
- Staged changes (`git diff --cached`) for commits
- Branch diff vs base (`origin/main`, `main`, or `master`) for DoD checks

## Project Rules (read before acting)
- `.cursor/rules/git-and-agile.mdc` — branch naming, Conventional Commits, DoD checklist
- `.cursor/rules/project-context.mdc` — artifacts that must never be committed

## Commit Workflow
1. Inspect `git diff --cached`; refuse if build artifacts or secrets are staged
2. Choose type (`feat`, `fix`, `refactor`, `docs`, `test`, `chore`) and scope from paths
3. Draft `type(scope): imperative summary` with optional body explaining **why**
4. Propose message only — do not run `git commit` unless user explicitly requests

## DoD Verification Workflow
1. Run `git diff <base>...HEAD --stat` to identify changed areas
2. Check each DoD item from `git-and-agile.mdc`:
   - Style, server tests, client lint, auth tests, docs, no artifacts, local testing
3. Run `cd server && npm test` if `server/` changed
4. Run `cd client && npm run lint` if `client/` changed
5. Produce pass/fail table with evidence per item

## Output Format
Commit proposal: message + staged file list + type/scope rationale.
DoD report: checklist table with ✅/❌ and summary of blockers.

## Done When
- Commit message follows Conventional Commits format from `git-and-agile.mdc`
- Every DoD item has a status and evidence citation
- No `git commit` or source edits unless explicitly requested
