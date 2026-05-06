# molecule-ai-plugin-molecule-skill-update-docs

After any code change, review recent edits and update all documentation:
architecture docs, API specs, edit history, README mirrors, runbooks, and
`.env.example`. Creates missing documentation for new implementations.

Run this skill after merging a PR that changes behavior, adds features, or
introduces new files.

**Version:** 1.0.0
**Runtime:** `claude_code`, `hermes`
**Skill:** `update-docs`

---

## What It Does (12-step workflow)

1. **Read today's edit history** — read `docs/edit-history/<date>.md` to find what changed today.
2. **Analyze changes** — read modified files; categorize as new feature, bug fix, architecture change, API change, or config change.
3. **Update edit-history session file** — add a summary at the top grouped under headings.
4. **Update CLAUDE.md** — new commands/scripts, architecture changes, new env vars, new routes/endpoints, test counts.
5. **Update PLAN.md** — mark completed phases, add follow-ups, keep current status in sync.
6. **Update README.md** — new user-visible features, setup changes, tech stack changes, test count badges.
7. **Update README.zh-CN.md** — mirror user-visible changes from README.md; keep translations in sync.
8. **Update .env.example** — every new env var must be documented with a comment; remove deprecated vars.
9. **Update docs/README.md** — new features, setup instructions, project overview.
10. **Update docs/ files** — check each doc for outdated sections; update or create as needed.
11. **Create new docs** — if a feature has no documentation, create appropriate docs following existing style.
12. **Report summary** — list all updated and created files.

---

## What Gets Updated

| Doc type | When to update |
|---|---|
| `CLAUDE.md` | New commands, architecture changes, env vars, test counts |
| `PLAN.md` | Completed phases, architectural decisions, next steps |
| `README.md` | User-visible features, setup changes, tech stack, badges |
| `README.zh-CN.md` | Mirror README.md changes; keep translations in sync |
| `.env.example` | Every new env var; remove deprecated vars |
| `docs/README.md` | New features, setup, project overview |
| `docs/<file>.md` | Architecture docs when features are added/removed/changed |
| `docs/edit-history/<date>.md` | Always updated at end of session |

---

## Repository Layout

```
molecule-skill-update-docs/
├── skills/
│   └── update-docs/
│       └── SKILL.md        # Full 12-step skill definition
├── adapters/
│   ├── __init__.py
│   └── claude_code.py     # AgentskillsAdaptor (wraps plugins_registry)
├── plugin.yaml             # Plugin manifest
└── README.md
```

---

## Key Conventions

| Topic | Convention |
|---|---|
| **When to run** | After merging a PR; explicitly triggered by `/update-docs` |
| **Edit history** | One session file per date: `docs/edit-history/YYYY-MM-DD.md` |
| **Env vars** | All vars read by code must be in `.env.example` with a comment |
| **README sync** | `README.zh-CN.md` must mirror `README.md` — never let them drift |
| **New docs** | Follow existing style and structure of the repo's docs |
| **Deprecations** | When removing features, mark as deprecated — do not silently delete docs |

---

## Development

```bash
# Verify docs/edit-history/ directory exists
ls docs/edit-history/

# Check for missing env var documentation
diff <(grep -h 'process.env' src/**/*.ts | sed 's/.*process.env.\([A-Z_]*\).*/\1/' | sort -u) \
     <(grep '^#\|^[A-Z]' .env.example | sed 's/ .*//' | sort -u)

# Run the skill (if Hermes/cron context)
# After a PR merge, invoke via the update-docs skill or /update-docs command
```

---

## Relationship to Other Plugins

- Used by `molecule-workflow-triage` — `/triage` workflow calls `update-docs` as a sub-step.
- Complements `molecule-audit-trail` — audit-trail records what changed; update-docs records the documentation impact.
- Pairs with `molecule-skill-cron-learnings` — learnings may flag docs that need updating.
