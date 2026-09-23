# /arch-review

## Purpose
Run an architecture review via the `architecture-review` skill on a design, PR, or proposed change.

## Inputs
- `$ARGUMENTS`: feature description, PR scope, or file paths to review
- If no arguments: review the current branch diff (`git diff origin/main...HEAD`)

## Steps
1. Read `.cursor/skills/architecture-review/SKILL.md` and follow its full workflow
2. Gather scope from `$ARGUMENTS` or `git diff origin/main...HEAD` (fallback: `main`, `master`)
3. Map affected layers (client, api, runtime, integrations, storage)
4. Check layering violations, circular deps, and boundary leaks per `architecture.mdc`
5. Assess scalability and at least 3 failure modes
6. Produce findings table with severities and remediations
7. Draft an ADR (Context / Decision / Consequences) if a design decision is unresolved

## Output Format
Architecture Review: Summary (risk level), Findings table, Layer Diagram, Scalability Notes, Failure Modes table, ADR (if needed).

## Stop Conditions
- **STOP and ask** if scope is unclear and there is no diff to review
- **STOP and ask** if the change is trivial (single-file cosmetic) and user wants a full review anyway

## Guardrails
- **Writes code: NO** — report and ADR draft only
- Do not modify any source files
