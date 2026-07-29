Skills are organized into bucket folders under `skills/`:

- `engineering/` — daily code work
- `productivity/` — daily non-code workflow tools
- `misc/` — kept around but rarely used
- `personal/` — tied to my own setup, not promoted
- `in-progress/` — drafts not yet ready to ship
- `deprecated/` — no longer used

Every skill in `engineering/`, `productivity/`, or `misc/` must have a reference in the top-level `README.md` and an entry in `.claude-plugin/plugin.json`. Skills in `personal/`, `in-progress/`, and `deprecated/` must not appear in either.

Each skill entry in the top-level `README.md` must link the skill name to its `SKILL.md`.

Each bucket folder has a `README.md` that lists every skill in the bucket with a one-line description, with the skill name linked to its `SKILL.md`.

## Using a `personal/` skill in Claude Code

`personal/` skills are excluded from `plugin.json`, so the `mattpocock-skills` plugin never loads them. To use one in Claude Code, link it into the standalone personal-skills folder (`~/.claude/skills/`, which Claude Code scans at startup):

```powershell
$link = "C:\Users\boris\.claude\skills\<skill-name>"
$target = "C:\Users\boris\Documents\GitHub\skills\skills\personal\<skill-name>"
if (-not (Test-Path "C:\Users\boris\.claude\skills")) { New-Item -ItemType Directory "C:\Users\boris\.claude\skills" | Out-Null }
New-Item -ItemType Junction -Path $link -Target $target
```

A directory junction (no admin needed) keeps the installed copy in sync with the repo — edit the file here, and the change is picked up on the next Claude Code restart. The skill loads as plain `/<skill-name>`, not under the plugin namespace. Remove with `Remove-Item $link` (deletes only the junction, not the source folder).

<!-- agent-memory-kit:governance -->
## Agent memory & self-improvement (repo-local)

This repo carries the **agent-memory-kit**. At the start of role work, consult `.agent-memory/roles/<role>/MEMORY.md`; at the end of meaningful work emit a `memory_proposal` block for reusable, evidence-backed learnings only. Only the architect or `memory-curator` promotes proposals. Role agents live in `.claude/agents/`; rules in `.claude/rules/memory-governance.md`. Maintenance: `/memory-maintain` or `python3 memory_maintainer.py --config .agent-memory/memory-maintainer.json --apply --json`. See `.agent-memory/README.md`.
