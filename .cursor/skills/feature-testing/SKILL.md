---
name: feature-testing
description: >-
  Derives test cases from acceptance criteria and implements them using FUXA's test
  framework (Mocha/Chai on server). Use when the user asks to write tests, create a
  test plan, verify a feature, or derive QA cases from acceptance criteria.
---

# Feature Testing

## When to Use
- User asks to test a feature, write test cases, or verify acceptance criteria
- After implementation, before PR — to close test gaps
- User provides Given/When/Then acceptance criteria needing automated coverage

## Inputs Needed
- Acceptance criteria (Given/When/Then) or user story from feature work
- Changed files or feature area (`server/api/`, `server/runtime/`, `client/`)
- Whether auth, device protocol, or storage logic is involved

## Project Rules (MUST follow)
- `.cursor/rules/testing-standards.mdc` — framework, naming, AAA, mocking policy
- `.cursor/rules/security-baseline.mdc` — auth test requirements
- `.cursor/rules/git-and-agile.mdc` — Definition of Done test criteria
- `.cursor/rules/design-patterns.mdc` — security test pattern (pattern #5)

## Workflow

1. **Parse acceptance criteria** — extract testable behaviors
2. **Derive test cases** — categorize each criterion:
   - Happy path
   - Edge cases (boundaries, empty input, max payload)
   - Negative cases (401, 403, 400, invalid input)
   - Regression (reproduce reported bug if applicable)
3. **Map to test location** — `server/test/<domain>/` per `testing-standards.mdc`
4. **Write tests** — Mocha + Chai; HTTP via `http.request`; AAA structure
5. **Run tests** — `cd server && npm test` (or targeted `npx mocha <file>`)
6. **Report gaps** — criteria without automated coverage + manual QA items
7. **Manual QA checklist** — browser steps for UI-only behavior

## Test Commands
```bash
cd server && npm test                          # full suite
cd server && npx mocha test/authorization/   # auth tests only
cd client && npm run lint                      # lint (no unit specs yet)
```

## Output Format

```markdown
# Test Plan: <feature>

## Acceptance Criteria → Test Cases
| # | Criterion | Type | Automated | Test File |
|---|-----------|------|-----------|-----------|
| 1 | Given..., When..., Then... | Happy | Yes | `server/test/.../foo.test.js` |

## Test Cases Detail
### TC-1: <name> (Happy)
- **Given**: ...
- **When**: ...
- **Then**: ...
- **Status**: [ ] Written [ ] Passing

## Gaps
- <criterion without automated test> → manual QA only

## Manual QA Checklist
- [ ] Start server (`cd server && npm start`), open http://localhost:1881
- [ ] <step-specific to feature>

## Run Results
```
<paste npm test output summary>
```
```

## Done When
- Every acceptance criterion maps to at least one test case or manual QA step
- Automated tests written in correct `server/test/` location and naming convention
- `npm test` executed; failures reported with fix suggestions
- Gaps explicitly listed; manual QA checklist provided for UI-only behavior
