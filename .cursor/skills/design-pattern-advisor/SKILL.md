---
name: design-pattern-advisor
description: >-
  Recommends design patterns for FUXA problems with trade-offs and minimal code
  sketches. Use when the user asks which pattern to use, how to structure new code,
  or needs architectural guidance for a specific implementation challenge.
---

# Design Pattern Advisor

## When to Use
- User asks "how should I implement X?" or "what pattern fits here?"
- New module design: device driver, API endpoint, Angular service, security check
- Refactoring decision between multiple valid approaches

## Inputs Needed
- Problem statement: what behavior is needed and by whom (UI, API, runtime, device)
- Constraints: performance, security, backward compatibility, testability
- Existing code context (file paths or feature area) if extending current code

## Project Rules (MUST follow)
- `.cursor/rules/architecture.mdc` — layering, import directions, code placement
- `.cursor/rules/design-patterns.mdc` — approved patterns and anti-patterns
- `.cursor/rules/coding-standards.mdc` — naming and style for sketches
- `.cursor/rules/security-baseline.mdc` — when auth or input handling is involved

## Workflow

1. **Restate the problem** — one sentence; identify which layer(s) are involved
2. **List 2–3 candidate patterns** — name each pattern and where it fits in FUXA
3. **Compare trade-offs** — complexity, testability, coupling, alignment with existing code
4. **Recommend one pattern** — justify against `architecture.mdc` and `design-patterns.mdc`
5. **Provide minimal code sketch** — 5–15 lines showing the recommended approach only
6. **Flag anti-patterns** — cite any `design-patterns.mdc` violations to avoid

## Output Format

```markdown
# Pattern Recommendation: <problem>

## Problem
<one-sentence restatement>

## Candidates

### Option A: <pattern name>
- **Fit**: <why it maps to FUXA layers>
- **Pros**: ...
- **Cons**: ...

### Option B: <pattern name>
...

### Option C: <pattern name>
...

## Recommendation
**Use Option <X>** because <alignment with architecture.mdc>.

## Minimal Sketch
```js
// 5-15 line example following design-patterns.mdc
```

## Anti-Patterns to Avoid
- <pattern from design-patterns.mdc NEVER list>
```

## Done When
- Exactly 2–3 candidates presented with honest trade-offs
- One clear recommendation tied to project architecture rules
- Sketch matches approved patterns (init injection, device driver, service+model, JWT auth, or security test)
- No full implementation — advisory only unless user then asks to implement
