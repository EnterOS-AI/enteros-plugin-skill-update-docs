# Test Rationale — molecule-skill-update-docs

## What this plugin does

`molecule-skill-update-docs` is a prose-only skill: its logic lives entirely in
`skills/update-docs/SKILL.md` (12-step documentation update workflow). The adapter
(`adapters/claude_code.py`) is a thin re-export of `AgentskillsAdaptor` from
`plugins_registry.builtins` — no business logic, no network calls, no side effects.

## What is tested

- `plugin.yaml` is valid YAML with required fields (name, version, runtimes, skills)
- `skills/update-docs/SKILL.md` has valid YAML frontmatter and a body with
  a Steps section documenting the update workflow
- `adapters/claude_code.py` exists and re-exports `AgentskillsAdaptor`
- `validate-plugin.py` (`.molecule-ci/scripts/`) exits zero

## What is NOT unit-tested (and why)

The documentation update workflow is prose guidance inside SKILL.md — no Python
function to unit test. Smoke tests cover the artifact structure; full evaluation
requires integration tests against a real workspace with filesystem access.

## Running tests

```bash
python -m pytest tests/ -v
```
