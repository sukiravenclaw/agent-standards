---
description: Load repo context (AGENTS.md, STATE.md, latest session log) and summarize where we are before doing any work
---

You are starting a new session in this repo. Do the following, in order, before touching any code.

1. Read `AGENTS.md` in full.
2. Read `STATE.md` in full. Pay closest attention to *Current focus*, *Data contracts*, *Open threads*, *Known issues*, *Last session*, and *Next actions*.
3. List `docs/sessions/` and read the most recent file. If the folder is empty or missing, say so.
4. Run `git log --oneline -15` and `git status`. Note any commits or uncommitted changes newer than the last session log — that is work that happened without a close-out and may not be reflected in `STATE.md`.

Then report back in this exact shape:

**Where we are** — one paragraph: current focus, which workstream, and what the last session concluded.

**Data contracts in force** — 3–6 bullets: population, outcome definition(s), time split, covariate lag, min cell size. Cite `STATE.md`. If any is marked `[UNKNOWN]`, list it.

**Drift check** — anything in git that postdates the last session log, or any contradiction between `STATE.md`, the latest session log, and the code. If none, say "No drift detected."

**Proposed first step** — the first item from *Next actions*, or your best inference if the list is empty, marked as inferred.

**Questions before I start** — only if genuinely blocking. Otherwise "None."

If the user passed arguments ($ARGUMENTS), treat them as today's goal and reconcile them with *Next actions* — say whether they match, extend, or diverge from the plan in `STATE.md`.

Do not start working until the user confirms.
