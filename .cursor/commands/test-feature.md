# /test-feature

## Purpose
Derive and implement tests via the `feature-testing` skill, then run the test suite and summarize failures.

## Inputs
- Acceptance criteria or user story (from chat, `$ARGUMENTS`, or a prior `/plan-feature` plan)
- Changed files or feature area to scope test coverage

## Steps
1. Read `.cursor/skills/feature-testing/SKILL.md` and follow its full workflow
2. Parse acceptance criteria into happy path, edge, negative, and regression test cases
3. Write tests in `server/test/<domain>/` using Mocha + Chai per `testing-standards.mdc`
4. Run `cd server && npm test` (or targeted `npx mocha <file>` for new tests only)
5. If client files changed, run `cd client && npm run lint`
6. Report gaps (criteria without automated coverage) and a manual QA checklist
7. Summarize all failures with file, test name, and suggested fix

## Files You May Touch
Only test files under `server/test/` and, if needed, test helper fixtures. Do not modify production source unless a test reveals a confirmed bug — ask first.

## Output Format
Test Plan with criteria mapping, test case details, gaps, manual QA checklist, and run results summary.

## Stop Conditions
- **STOP and ask** if no acceptance criteria or feature description is provided
- **STOP and ask** before fixing production code revealed by failing tests
- **STOP and ask** if tests require new npm dependencies

## Guardrails
- **Writes code: YES** — test files only (`server/test/**`)
- MUST run `npm test` after writing tests and report pass/fail summary
