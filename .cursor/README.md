# FUXA Cursor Configuration

## Directory Tree

```
.cursor/
├── rules/           # Persistent constraints (auto-applied by glob or always)
│   ├── project-context.mdc
│   ├── architecture.mdc
│   ├── coding-standards.mdc
│   ├── design-patterns.mdc
│   ├── testing-standards.mdc
│   ├── git-and-agile.mdc
│   └── security-baseline.mdc
├── skills/          # Workflow playbooks (agent reads on demand)
│   ├── feature-development/
│   ├── code-analysis/
│   ├── design-pattern-advisor/
│   ├── architecture-review/
│   ├── pr-review/
│   ├── feature-testing/
│   └── git-workflow/
├── commands/        # Slash commands (type / in Agent chat)
│   ├── plan-feature.md
│   ├── implement.md
│   ├── analyze.md
│   ├── pattern.md
│   ├── arch-review.md
│   ├── pr-review.md
│   ├── test-feature.md
│   ├── commit.md
│   └── dod-check.md
└── agents/          # Delegatable subagents (read-only)
    ├── code-reviewer.md
    └── test-verifier.md
```

## Rules (constraints — not workflows)

| Rule | Trigger | Purpose |
|------|---------|---------|
| `project-context.mdc` | Always | Stack, folder map, commands, NEVER-do list |
| `architecture.mdc` | `client/src/**`, `server/**` | Layering, import directions |
| `coding-standards.mdc` | `**/*.ts`, `**/*.js`, `**/*.html` | Formatting, naming, logging |
| `design-patterns.mdc` | Description-triggered | Approved patterns + anti-patterns |
| `testing-standards.mdc` | `**/*test*`, `**/*spec*` | Mocha conventions, AAA, mocking |
| `git-and-agile.mdc` | Always | Branches, commits, DoD, user stories |
| `security-baseline.mdc` | Always | Auth, secrets, input validation |

## Skills (workflows — reference rules, don't duplicate them)

| Skill | Used by |
|-------|---------|
| `feature-development` | `/plan-feature`, `/implement` |
| `code-analysis` | `/analyze` |
| `design-pattern-advisor` | `/pattern` |
| `architecture-review` | `/arch-review` |
| `pr-review` | `/pr-review`, `code-reviewer` agent |
| `feature-testing` | `/test-feature` |
| `git-workflow` | `/commit`, `/dod-check` |

## Subagents

| Agent | Mode | Purpose |
|-------|------|---------|
| `code-reviewer` | `readonly: true` | PR/diff review via `pr-review` skill |
| `test-verifier` | `readonly: true` | Runs `npm test` / `npm run lint`, reports pass/fail |

## Worked Example: Add a Password-Reset Endpoint

```
1. /plan-feature Add POST /api/auth/reset-password with email token flow
   → Outputs Plan.md: user story, acceptance criteria, impact on
     server/api/auth/, server/runtime/users/, client login UI. STOPS for approval.

2. /implement
   → Implements approved tasks; touches only listed files + server/test/authorization/.
   → Runs npm test and npm run lint.

3. /test-feature
   → Derives tests from acceptance criteria; writes server/test/authorization/resetPassword.test.js.
   → Runs npm test; reports gaps + manual QA checklist.

4. /pr-review
   → Reviews git diff vs origin/main; checks security-baseline, architecture, tests.

5. /dod-check
   → Verifies all 7 DoD items from git-and-agile.mdc with evidence.

6. /commit  (optional, after staging)
   → Proposes: feat(api): add password reset endpoint with token expiry
```

## Adding a New Skill

1. Create `.cursor/skills/<skill-name>/SKILL.md`
2. Add YAML frontmatter: `name` (kebab-case) and `description` (include WHEN-to-use triggers)
3. Include: When to Use, Inputs, numbered steps, Output format, Done When
4. Reference `.cursor/rules/*.mdc` — do **not** duplicate rule content
5. Keep under 120 lines; one concern per skill
6. Optionally add a matching `/command` in `.cursor/commands/<name>.md` that invokes the skill
7. Update this README's tables

## Priority Order

When instructions conflict: **safety rules** → **repo rules** → **skill instructions** → **ad-hoc prompts**
