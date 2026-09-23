---
name: feature-development
description: >-
  Guides end-to-end FUXA feature delivery from requirements through implementation
  and Definition of Done. Use when the user asks to build a new feature, implement
  a user story, plan a change, or start development work on client or server code.
---

# Feature Development

## When to Use
- User requests a new feature, enhancement, or multi-file change
- Work spans `client/` and/or `server/` and needs planning before coding
- User asks for a user story, task breakdown, or implementation plan

## Inputs Needed
- Feature description or user story (or ask the user to provide one)
- Affected area: UI (`client/src/app/`), API (`server/api/`), runtime (`server/runtime/`), docs
- Constraints: backward compatibility, security, performance, release timeline

## Project Rules (read before acting)
- `.cursor/rules/project-context.mdc` — stack, commands, NEVER-do list
- `.cursor/rules/architecture.mdc` — layering, where new code belongs
- `.cursor/rules/coding-standards.mdc` — formatting, naming, error handling
- `.cursor/rules/design-patterns.mdc` — approved patterns
- `.cursor/rules/git-and-agile.mdc` — branches, commits, Definition of Done
- `.cursor/rules/security-baseline.mdc` — auth, secrets, validation

## Workflow

1. **Clarify requirements** — ask targeted questions; resolve ambiguities before coding
2. **Write user story + acceptance criteria** — use format from `git-and-agile.mdc`
3. **Impact analysis** — list files/modules to touch; flag cross-layer changes
4. **Task breakdown** — ordered tasks with rough estimates (S/M/L); identify risks
5. **Present plan** — output Plan.md checklist; wait for user approval unless told to proceed
6. **Implement** — small, focused commits per `git-and-agile.mdc`; follow `architecture.mdc` boundaries
7. **Add tests** — follow `testing-standards.mdc`; auth changes need `server/test/authorization/` tests
8. **Self-check** — run `cd server && npm test` and/or `cd client && npm run lint`; verify DoD checklist

## Output Format

Produce a Plan.md-style checklist:

```markdown
# Feature: <title>

## User Story
As a <role>, I want <capability>, so that <benefit>.

## Acceptance Criteria
- [ ] Given <pre>, When <action>, Then <outcome>

## Impact Analysis
| Area | Files / Modules | Risk |
|------|-----------------|------|
| client | `client/src/app/...` | Low/Med/High |

## Task Breakdown
- [ ] (S) Task 1 — ~30 min
- [ ] (M) Task 2 — ~2 hr

## Implementation Progress
- [ ] Plan approved
- [ ] Code implemented
- [ ] Tests added and passing
- [ ] Lint clean
- [ ] Definition of Done met (see git-and-agile.mdc)
```

## Done When
- All acceptance criteria have corresponding implementation and tests
- `npm test` (server) and/or `npm run lint` (client) pass for touched areas
- Definition of Done checklist in `git-and-agile.mdc` is fully satisfied
- No build artifacts or secrets committed
