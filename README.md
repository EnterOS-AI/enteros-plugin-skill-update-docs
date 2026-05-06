# molecule-skill-update-docs — Documentation Sync

Plugin for Claude Code and Hermes. After any code change, review recent edits and
update all documentation: architecture docs, API specs, runbooks, edit history, and
README mirrors. Creates missing docs for new implementations.

## When to use

After merging a PR that changes behavior, adds features, or introduces new files.
Run the `update-docs` skill to audit what docs need updating.

## What it updates

| Doc type | What to check |
|----------|---------------|
| Architecture docs | New components, changed data flows, updated dependencies |
| API specs | New endpoints, changed request/response shapes, auth changes |
| Edit history | Session log entry with what changed and why |
| README mirrors | Updated descriptions of plugin capabilities |
| Runbooks | Updated operational procedures after incidents or changes |

## Installation

### In org template (org.yaml)
```yaml
plugins:
  - molecule-skill-update-docs
```

### From URL
```
github://Molecule-AI/molecule-ai-plugin-molecule-skill-update-docs
```

## License
Business Source License 1.1 — © Molecule AI.
