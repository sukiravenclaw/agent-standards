---
description: Scaffold AGENTS.md, STATE.md, README.md, CLAUDE.md and docs/ in this repo from the shared templates, then fill them in
---

You are setting up this repo for continuous, iterative agent work using the shared standards in `~/GitHub/agent-standards/`. Follow the steps in order.

## 1. Check what's here

Run `ls -la`, `git log --oneline -20 2>/dev/null`, and look for any existing `AGENTS.md`, `STATE.md`, `CLAUDE.md`, `README.md`, `docs/`. 
- If `STATE.md` already exists, stop and tell me — this repo may already be set up; ask whether I want to re-initialize.
- Classify the repo: **empty/new** (no meaningful code or history) or **existing** (has code, notebooks, or history).

## 2. Scaffold

Copy templates without overwriting anything that already exists:
- `~/GitHub/agent-standards/templates/AGENTS.md` → `./AGENTS.md`
- `~/GitHub/agent-standards/templates/STATE.md` → `./STATE.md`
- `~/GitHub/agent-standards/templates/CLAUDE.md` → `./CLAUDE.md`
- `~/GitHub/agent-standards/templates/README.md` → `./README.md` (if no README exists; if one exists, add the "If you are an AI agent" block near the top instead)
- Create `docs/decisions/.gitkeep`, `docs/sessions/.gitkeep`, and `outputs/.gitkeep`, `notebooks/`, `src/`, `tests/` if missing.
- Ensure `.gitignore` covers `data/`, `.env`, `.venv/`, `__pycache__/`, `*.pkl` unless the repo intentionally commits models.

## 3. Interview me (briefly)

Ask, in one message, only what you can't infer from the repo:
1. What question(s) does this repo answer, and for whom?
2. Workstreams (1–3), one line each.
3. What is explicitly out of scope / lives in a sibling repo?
4. Data source(s), population, outcome definition(s), time unit, min cell size — whatever applies.
5. Any rules that add to or override the global ones?
6. The first 1–3 things you want done.

If the argument `$ARGUMENTS` was passed, treat it as the answer to question 1 and skip it.

## 4. Fill the files

Using my answers and anything you found in step 1:
- `AGENTS.md`: fill every section. Keep it repo-specific; anything universal belongs in the global file — say so rather than adding it.
- `STATE.md`: replace every bracketed placeholder with real content or `[UNKNOWN — ask Suki: <question>]`. Set *Current focus* and *Next actions* from my answers.
- `README.md`: fill the overview, layout, setup, run commands.

**If the repo is existing** (not empty): before filling, run the audit — read the tree, notebooks, scripts, artifacts, and full `git log`; find every cohort/outcome/split/threshold definition and every model artifact; write `docs/_audit_YYYY-MM-DD.md` and show it to me before filling the files. Then backfill 3–8 decision records into `docs/decisions/` from history, with evidence cited and unknown reasons marked unknown.

## 5. Baseline session log and commit

- Write `docs/sessions/YYYY-MM-DD_init.md` describing the initial state so the next `/open-session` has something to read.
- Commit: `chore: initialize agent context (AGENTS.md, STATE.md, docs/)`.
- Run `/memory` and confirm the global file and this repo's `CLAUDE.md` both load.

## 6. Report

≤5 bullets: what was created, the `[UNKNOWN]` list for me to answer, and the first item in *Next actions*. Then stop — I'll start real work with `/open-session`.
