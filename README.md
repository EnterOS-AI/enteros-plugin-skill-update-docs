# molecule-skill-update-docs — Documentation Sync

Plugin for Claude Code and Hermes. After any code change, review recent edits and
update all documentation: architecture docs, API specs, runbooks, edit history, and
README mirrors. Creates missing docs for new implementations.

## When to use

Before merging a PR that changes behavior, adds features, or introduces new files,
run the `update-docs` skill so documentation ships with the implementation.

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
gitea://molecule-ai/molecule-ai-plugin-molecule-skill-update-docs#main
```

## License
Business Source License 1.1 — © Molecule AI.
