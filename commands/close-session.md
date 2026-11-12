---
description: Write the session log, update STATE.md, and record any decisions so the next session can pick up with full context
---

The session is ending. Close it out so nothing is lost. Do all of the following; do not skip steps because the session was short.

## 1. Reconstruct what happened this session

From the conversation, uncommitted changes, and `git log` since the session started, list: what was attempted, what was completed, what was learned, what didn't work, and any choices made that a future agent would need to know about.

## 2. Write the session log

Create `docs/sessions/YYYY-MM-DD_<short-topic>.md` (today's date; if one already exists for today, append a suffix `-2`, `-3`). Use the template from the global instructions §7:

```
# Session — YYYY-MM-DD — <topic>
Goal:
What was done:        (bullets; reference files and commits)
Results:              (numbers with intervals and n; link outputs/ paths)
Decisions made:       (link decision records)
Dead ends:            (what didn't work and why — be specific, this saves the next agent hours)
Open questions for Suki:
Next actions:         (ordered)
```

Be concrete. "Tuned the model" is useless; "Tried monotone constraints on tenure in D-01; AUC unchanged (0.81 → 0.81), dropped it" is useful.

## 3. Record decisions

For every non-trivial choice made this session (model family, feature definition, exclusion rule, threshold, data contract change) that doesn't already have a record: create `docs/decisions/NNNN_<slug>.md` using the global §6 template, with the next sequential number. Cite evidence. If a previous decision was overturned, set its status to `superseded by NNNN`.

## 4. Update STATE.md

Edit in place; preserve structure. Update:
- **Last updated** line at the top
- **Current focus** and **Status at a glance** if they changed
- **Data contracts** — only if a contract changed, and only if there is a decision record for it
- **Model registry** — new, promoted, or retired models
- **Decision log** — one row per new decision
- **Open threads** — add new ones, remove closed ones
- **Known issues / gotchas** — anything discovered this session
- **Questions waiting on Suki** — from the session log
- **Last session** — date, log path, 3–6 bullets
- **Next actions** — replace the list with the ordered list from the session log

## 5. Promote universal lessons

If any correction Suki made this session is about how agents should work in *every* repo (not just this one), do not put it in `AGENTS.md`. Instead, propose the exact edit to `~/GitHub/agent-standards/CLAUDE.md` and ask before applying. If a lesson is repo-specific but durable, add it to `AGENTS.md` → *Gotchas*.

## 6. Commit

Stage `docs/` and `STATE.md` (and `AGENTS.md` if edited). Commit with message `session: YYYY-MM-DD <topic>`. Do not commit code, notebooks, or outputs in this commit unless Suki asks — those get their own commits.

## 7. Report

≤5 bullets: what changed in the repo, what's in *Next actions*, any question blocking the next session. Then stop.

If the user passed arguments ($ARGUMENTS), treat them as extra notes to fold into the session log.
