---
name: architecture-review
description: >-
  Reviews FUXA changes or designs for layering violations, circular dependencies,
  boundary leaks, scalability, and failure-mode risks. Use when the user asks for an
  architecture review, ADR, system design check, or scalability/failure analysis.
---

# Architecture Review

## When to Use
- User proposes a new subsystem, cross-cutting change, or significant refactor
- User asks "will this scale?" or "what happens when X fails?"
- Pre-merge review of multi-module changes touching `client/` and `server/`

## Inputs Needed
- Scope: PR diff, design proposal, or feature description
- Expected load or deployment context (embedded, Docker, multi-user) if known
- Failure scenarios of concern (device disconnect, DB loss, auth outage)

## Project Rules (MUST enforce)
- `.cursor/rules/architecture.mdc` — layering and import boundaries
- `.cursor/rules/design-patterns.mdc` — approved vs forbidden patterns
- `.cursor/rules/security-baseline.mdc` — auth and data boundary leaks
- `.cursor/rules/project-context.mdc` — runtime constraints

## Workflow

1. **Map affected layers** — client, api, runtime, integrations, storage
2. **Check layering violations** — runtime→api imports, client→protocol direct calls
3. **Detect circular dependencies** — require/import cycles between modules
4. **Identify boundary leaks** — secrets, device credentials, or internal state exposed via API
5. **Assess scalability** — socket fan-out, DAQ write throughput, storage growth, blocking I/O
6. **Analyze failure modes** — what happens on timeout, crash, partial write, auth failure
7. **Produce findings table** — severity, location, risk, remediation
8. **Draft ADR** (if a design decision is needed) — Context / Decision / Consequences

## Output Format

```markdown
# Architecture Review: <scope>

## Summary
<overall risk: Low / Medium / High>

## Findings
| Severity | Location | Issue | Risk | Remediation |
|----------|----------|-------|------|-------------|
| Blocker | `server/runtime/x.js` | Imports from api/ | Circular dep | Extract to runtime/utils |
| Major | ... | ... | ... | ... |
| Minor | ... | ... | ... | ... |

## Layer Diagram
<mermaid: client → api → runtime → devices/storage>

## Scalability Notes
- ...

## Failure Modes
| Scenario | Current Behavior | Risk | Recommendation |
|----------|-----------------|------|----------------|

## ADR (if decision needed)
### Context
<forces and constraints>
### Decision
<chosen approach>
### Consequences
<positive and negative outcomes>
```

## Done When
- All layering rules from `architecture.mdc` are explicitly checked
- Findings table is complete with severities and remediations
- Scalability and at least 3 failure modes are considered
- ADR drafted when the review surfaces an unresolved design choice
