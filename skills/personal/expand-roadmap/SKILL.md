---
name: expand-roadmap
description: Push one of Boris's project roadmaps forward — break a phase into concrete tasks, draft the next sprint sized to his solo evenings-only capacity, extend the roadmap horizon with new future phases, and surface the open decisions he still owns as [TBC]. Knows the Native FMS phase ladder, the Encompass M0–M8 milestones, and the flc-strategic-2026 playbook. Use when Boris wants to expand or extend a roadmap, plan or draft a sprint, break a phase into tasks, decide what to build next, or says /expand-roadmap.
---

# Expand Roadmap

Take one of Boris's existing roadmaps and move it forward: break phases into tasks, draft the next sprint, extend the horizon, and flag the decisions he still owns. **Always propose in chat first; only write back to the file once Boris approves.**

## Roadmaps this operates on

Read the live file before proposing anything — these move, so confirm the path.

| Roadmap | Shape | Location |
|---|---|---|
| Native FMS | Phase ladder (1–5) + critical path + sequencing | `Desktop\Desktop\FLC\Projects\Main FLC Projects\Native FMS\ROADMAP.md` |
| Encompass | Milestone ladder M0–M8 | Encompass repo (milestones) |
| FLC strategic 2026 | Project matrix + dated gates + metrics + review log | `life-os\playbooks\flc-strategic-2026.md` |

If a path has moved, Glob for `ROADMAP.md` or the playbook before asking Boris where it is.

## Ground rules

- **Resource model:** Boris solo, evenings only. Size everything in **eng-days**, the unit his roadmaps already use. Bias to under-scoping — a "sprint" is a realistic block of evenings, not a team's two weeks.
- **Critical path only:** propose work that is *unblocked*. State the critical path explicitly and never queue decorative or blocked items (e.g. Native FMS Phase 5 Layers 2+3 are meaningless before the Phase 4 backend lands).
- **Never assume dates or numbers:** every date, € figure, budget, or commercial number is `[TBC]`. Boris sets these against context you don't see — do not invent them.
- **Match the file's own format:** mirror its existing table columns, phase numbering, and tone. Keep framing/beneficiary columns on stakeholder-facing roadmaps (the playbook); keep effort/dependency/done columns on build roadmaps (Native FMS, Encompass).

## Workflows

Start every workflow by **reading the roadmap and restating current state** — done / in-flight / queued / blocked — so you and Boris are aligned before you expand anything.

### 1. Draft next sprint
1. Confirm the window and available evening hours, then convert to an eng-day budget.
2. Pull the next unblocked items off the critical path.
3. Fit to budget (under, not over) and state one clear sprint goal.
4. Output: ordered tasks, each with an eng-day estimate and a definition of done; running total ≤ budget; an explicit **"not this sprint"** list.

### 2. Expand a phase into tasks
Break the chosen phase into concrete deliverables. Per task: eng-day estimate, dependencies (what must land first), risk, and definition of done. Flag any task that hides a decision Boris owns.

### 3. Extend the horizon
Propose phases or milestones beyond the current end. Per new phase: what unlocks it (sequencing), rough effort, the capability it adds, and `[TBC]` for anything needing a date or budget. Don't invent a timeline.

### 4. Surface open decisions
Collect every fork Boris owns — pitch/ship dates, budget envelopes, sequencing choices, scope toggles — as a `[TBC]` checklist. Never fill these in yourself.

## Writing back (only after approval)

- Append a clearly marked `## Proposed — <date>` section, or edit where Boris directs. Never silently rewrite existing lines.
- If the roadmap lives in a git submodule (e.g. Encompass), cd into the submodule rather than editing from the vault. For any pushed repo, use a feature branch and scrub personal identifiers before committing.
- If the roadmap has a review log, add a dated bullet (newest on top) noting what changed.
