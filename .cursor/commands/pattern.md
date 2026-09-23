# /pattern

## Purpose
Get a design pattern recommendation via the `design-pattern-advisor` skill for an implementation challenge.

## Inputs
- `$ARGUMENTS`: problem statement or "how should I implement X?" question
- Optional: file paths or feature area for context

## Steps
1. Read `.cursor/skills/design-pattern-advisor/SKILL.md` and follow its full workflow
2. Parse the problem from `$ARGUMENTS` or ask the user to describe it
3. Identify which FUXA layer(s) are involved (client, api, runtime, integrations)
4. Present 2–3 candidate patterns with trade-offs
5. Recommend one aligned with `.cursor/rules/architecture.mdc` and `design-patterns.mdc`
6. Provide a minimal 5–15 line code sketch; flag anti-patterns to avoid

## Output Format
Pattern Recommendation: Problem, Candidates (A/B/C with pros/cons), Recommendation, Minimal Sketch, Anti-Patterns to Avoid.

## Stop Conditions
- **STOP and ask** if the problem statement is too vague to identify a layer
- **STOP and ask** if multiple unrelated problems are bundled (ask user to pick one)
- Do not implement full code unless the user explicitly requests it afterward

## Guardrails
- **Writes code: NO** — advisory report and sketch only
- Do not modify any source files
