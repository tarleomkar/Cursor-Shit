# /plan-feature

## Purpose
Run the **planning phase only** of the `feature-development` skill. Produce a Plan.md checklist and **stop for user approval** before any code is written.

## Inputs
- Feature description, user story, or bug report (from chat or `$ARGUMENTS`)
- Optional: affected area (`client/`, `server/`, `docs/`), constraints, deadline

## Steps
1. Read `.cursor/skills/feature-development/SKILL.md` and follow its workflow **steps 1–5 only**
2. Read referenced rules in `.cursor/rules/` as needed (do not duplicate their content)
3. Ask clarifying questions if requirements are ambiguous
4. Write user story + Given/When/Then acceptance criteria (format from `git-and-agile.mdc`)
5. Produce impact analysis: list files/modules to touch with risk ratings
6. Break work into ordered tasks with S/M/L estimates
7. Output the Plan.md checklist from the skill's Output Format section
8. **STOP** — do not write or edit any source files

## Output Format
Plan.md-style checklist with unchecked boxes: User Story, Acceptance Criteria, Impact Analysis table, Task Breakdown, Implementation Progress (all unchecked).

## Stop Conditions
- **STOP and ask** if the feature scope is unclear or spans unrelated subsystems
- **STOP and ask** if security/auth implications are unknown
- **STOP and ask** if the user has not described what "done" looks like
- **STOP after plan output** — wait for explicit user approval before `/implement`

## Guardrails
- **Writes code: NO** — report and plan only
- Do not run builds, tests, or modify any files
