---
name: code-analysis
description: >-
  Performs read-only codebase analysis: maps entry points, dependencies, complexity
  hotspots, duplication, dead code, and coupling. Use when the user asks to analyze,
  audit, understand, or explore code structure, or requests a health/complexity report.
---

# Code Analysis

## When to Use
- User asks to understand how a module, feature, or flow works
- User requests a complexity audit, dead-code scan, or dependency map
- Pre-refactor exploration before any code changes

## Inputs Needed
- Scope: file path, feature name, or subsystem (e.g. `jwt-helper`, `server/runtime/devices/modbus`)
- Depth: quick overview vs thorough analysis
- Focus areas (optional): performance, security, maintainability

## Project Rules (reference for context)
- `.cursor/rules/project-context.mdc` — folder map, entry points
- `.cursor/rules/architecture.mdc` — expected layering and import directions

## Workflow

1. **Identify entry points** — `server/main.js`, `client/src/main.ts`, API routers, Socket.io handlers
2. **Map dependencies** — trace `require()` / `import` chains; note cross-layer calls
3. **Find complexity hotspots** — large files, deep nesting, high cyclomatic areas, god modules
4. **Detect duplication** — copy-pasted logic, parallel implementations of same concern
5. **Flag dead code** — unreferenced exports, unreachable branches, commented-out blocks
6. **Assess coupling** — circular deps, runtime→api violations, client bypassing services
7. **Report findings** — severity-rated list with `file:line` refs and suggested fixes

**IMPORTANT: Report only. Do NOT modify code.**

## Output Format

```markdown
# Code Analysis: <scope>

## Summary
<2-3 sentences on overall health>

## Entry Points
| Entry | Path | Role |
|-------|------|------|

## Dependency Map
<mermaid or bullet list of key imports>

## Findings

### Blockers
| # | Location | Issue | Suggested Fix |
|---|----------|-------|---------------|
| 1 | `server/api/foo.js:42` | runtime→api import | Move shared logic to runtime/utils |

### Major
| # | Location | Issue | Suggested Fix |

### Minor
| # | Location | Issue | Suggested Fix |

## Metrics (approximate)
- Files analyzed: N
- Largest file: `path` (lines)
- Coupling violations: N
```

## Done When
- Every finding has a severity (Blocker / Major / Minor), `file:line` reference, and actionable fix
- Entry points and dependency flow are documented
- No source files were modified
