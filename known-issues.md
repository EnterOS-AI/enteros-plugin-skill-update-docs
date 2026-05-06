# Known Issues

Active and recently resolved issues for `molecule-skill-update-docs`.

---

## Active Issues

*(None currently open. File an issue if you encounter a problem.)*

---

## Known Gotchas

### README.zh-CN.md sync can drift silently

**Severity:** Medium
**Detail:** The skill updates README.zh-CN.md after README.md but does not independently verify that translations remain accurate — it mirrors the English text into Chinese sections, but does not re-translate. If a developer edits README.zh-CN.md directly (e.g., to correct a translation), subsequent `update-docs` runs may overwrite those corrections.

**Workaround:** Keep corrections in a separate `docs/translation-notes.md` file that the skill is instructed to preserve. Alternatively, review README.zh-CN.md changes before committing.

---

### `.env.example` detection is heuristic — false negatives possible

**Severity:** Low
**Detail:** The skill uses `process.env` pattern matching to find env vars in source code. This approach can miss:
- Vars read via `os.environ["VAR"]` (Python)
- Vars accessed via `os.Getenv("VAR")` (Go)
- Vars injected at build time (Webpack, Vite)
- Vars accessed via a config struct that is populated from env at runtime

**Workaround:** Manually audit `.env.example` after adding new configuration. Use `grep -r 'ENV\|env\|getenv\|environ' src/ | grep -v '.env.example'` to find additional vars the skill might miss.

---

### No automatic invocation — must be triggered explicitly

**Severity:** Informational
**Detail:** The skill does not auto-run. It must be explicitly invoked (via `/update-docs` command or skill call). In CI/CD workflows, this means docs can become stale between runs if developers forget to invoke the skill.

**Workaround:** Add a CI step that warns (not fails) if `git diff --name-only` shows doc-relevant files were modified but `docs/edit-history/` was not updated in the same PR.

---

### docs/edit-history/ date-based naming requires timezone awareness

**Severity:** Low
**Detail:** The edit history file is named by date (`YYYY-MM-DD`). The date used is derived from the system clock at the time of the run. In distributed cron setups across timezones, the same work session may log to two different date files.

**Workaround:** Use UTC consistently for `docs/edit-history/` file naming, regardless of local timezone.

---

## Recently Resolved

*(None yet.)*
