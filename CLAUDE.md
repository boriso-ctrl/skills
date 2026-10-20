Skills are organized into bucket folders under `skills/`:

- `engineering/`: daily code work
- `productivity/`: daily non-code workflow tools
- `misc/`: kept around but rarely used, not promoted
- `in-progress/`: beta: public on purpose, feedback wanted, not shipped in the plugin
- `deprecated/`: no longer used

Every skill in `engineering/` or `productivity/` (the **promoted** buckets) must have a reference in the top-level `README.md` and an entry in `.claude-plugin/plugin.json`'s `skills` array (the Claude Code plugin ships exactly the promoted set). Skills in `misc/`, `in-progress/`, and `deprecated/` must not appear in either.

Install commands are copied verbatim from [.agents/install-block.md](./.agents/install-block.md). `.claude-plugin/marketplace.json` makes the repo its own single-plugin marketplace (a fallback the install block explains, not the documented route). Run `claude plugin validate . --strict` after touching either manifest. Why a Claude plugin but not (yet) a Codex one lives in [.agents/adr/0002-ship-as-a-claude-code-plugin.md](./.agents/adr/0002-ship-as-a-claude-code-plugin.md).

Each skill entry in the top-level `README.md` must link the skill name to its `SKILL.md`.

Each bucket folder has a `README.md` that lists every skill in the bucket with a one-line description, with the skill name linked to its `SKILL.md`. The promoted buckets' `README.md`s and the top-level `README.md` group entries into **User-invoked** and **Model-invoked**; non-promoted bucket `README.md`s (`misc/`, `in-progress/`) use a flat list.

Skills in `engineering/` and `productivity/` also have a human-facing docs page at `docs/<bucket>/<skill-name>.md` (the docs tree mirrors those two bucket folders under `skills/`). The published URL is `https://aihero.dev/skills-<skill-name>` regardless of bucket: the docs path is repo organisation only. When you add, rename, or change the behaviour of a skill in `engineering/` or `productivity/`, create or re-sync its docs page following [.agents/writing-docs.md](./.agents/writing-docs.md). A finished page carries four sections: **What it does**, **When to reach for it**, **Common questions**, and **It's working if**. `writing-docs.md` holds the template, the section order, and where to hunt for the questions. Skills in the non-promoted buckets (`misc/`, `in-progress/`, `deprecated/`) get **no** docs page.

Every `SKILL.md` is either user-invoked (`disable-model-invocation: true` plus `policy.allow_implicit_invocation: false` in `agents/openai.yaml`, reachable only by the human) or model-invoked (model- or user-reachable). See [.agents/invocation.md](./.agents/invocation.md).

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md) is the router that maps every user-reachable skill and how they relate. The same trigger that re-syncs a docs page applies to it: whenever you add, rename, remove, or change how a user-reachable skill fits the flows, re-read `ask-matt`'s `SKILL.md` and update it so the map stays accurate: a new skill it never mentions, or a stale one it still routes to, is a router that lies.

To (re)link every skill outside `deprecated/` and `misc/` into the local harness skill directories (`~/.claude/skills`, `~/.agents/skills`), run `scripts/link-skills.sh`. Each entry is a symlink into this repo, so a `git pull` keeps installed skills current; re-run the script after adding, removing, or renaming a skill.

No em-dashes anywhere in this repo's prose (`SKILL.md` files, docs, `README.md`, `CHANGELOG.md`, ADRs, changesets, code comments). Where a sentence reaches for one, rewrite it instead with a comma, colon, period, parentheses, or a conjunction, whichever the sentence actually wants; never do a blind character substitution.

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

This repo carries the **agent-memory-kit**. At the start of role work, consult `.agent-memory/roles/<role>/MEMORY.md`; at the end of meaningful work emit a `memory_proposal` block for reusable, evidence-backed learnings only. Only the architect or `memory-curator` promotes proposals. Role agents live in `.claude/agents/`; rules in `.claude/rules/memory-governance.md`. Maintenance: `/memory-maintain` or `python3 memory_maintainer.py --config .agent-memory/memory-maintainer.json --apply --json`. See [.agent-memory/README.md](./.agent-memory/README.md) and [.agent-memory/GOVERNANCE.md](./.agent-memory/GOVERNANCE.md) (promotion targets, proposal format, self-improvement loop, tool adapters).