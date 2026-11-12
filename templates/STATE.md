# STATE.md — Attrition Analytics

> **Living document. Update at the end of every session.** See `AGENTS.md` §5.
> Everything in `[brackets]` is a placeholder Suki needs to fill on first setup.
> Last updated: `[YYYY-MM-DD]` by `[Suki / agent]`

---

## Current focus

`[One or two sentences. What is the active question right now? Which workstream (A. Forecasting / B. Drivers)?]`

## Status at a glance

| Workstream | Stage | Blocked? | Owner of next step |
|---|---|---|---|
| A. Forecasting | `[exploration / modeling / validation / reporting / maintenance]` | `[no / yes — why]` | `[Suki / agent]` |
| B. Drivers | `[exploration / modeling / validation / reporting / maintenance]` | `[no / yes — why]` | `[Suki / agent]` |

## Data contracts

These are the definitions every analysis must use. Change them only via a decision record.

- **Data source(s):** `[table / pipeline names; owner team]`
- **Snapshot cadence:** `[e.g., weekly pull, Monday]` — current snapshot ID: `[ ]`
- **Population:** `[e.g., FTE only; excludes contractors and interns; excludes tenure < 30 days]`
- **Outcome definition:**
  - Voluntary attrition: `[termination reason codes = …]`
  - Involuntary attrition: `[… ]` — **modeled separately**
  - Censoring date: `[= snapshot date]`
- **Time unit:** `[month / week]` for forecasting; `[days of tenure]` for survival
- **Time split:** train `[through YYYY-MM]`, validation `[YYYY-MM to YYYY-MM]`, holdout `[from YYYY-MM]`
- **Covariate lag:** `[e.g., all covariates measured ≥ 1 month before period start]`
- **Minimum reporting cell size:** `[n = ]`
- **Known leakage fields (excluded):** `[list]`
- **Segments in scope:** `[org, level, tenure band, location, manager span …]`

## Model registry

| ID | Workstream | Type | Status | Key metric | Location | Notes |
|---|---|---|---|---|---|---|
| `[F-01]` | A | `[e.g., Cox w/ TVC → headcount projection]` | `[draft/candidate/champion/retired]` | `[e.g., MAPE on holdout, with CI]` | `[path]` | |
| `[F-02]` | A | `[e.g., time-series baseline (ETS/ARIMA)]` | | | | |
| `[D-01]` | B | `[XGBoost + SHAP]` | | `[AUC / PR-AUC]` | | |
| `[D-02]` | B | `[HGB ensemble]` | | | | |
| `[D-03]` | B | `[Cox PH — hazard drivers]` | | `[c-index]` | | |
| `[C-01]` | B | `[DiD — stock price × attrition]` | | `[effect + CI; parallel-trends check]` | | |

## Decision log

Newest first. Full records in `docs/decisions/`.

| # | Date | Decision | Status |
|---|---|---|---|
| `[0001]` | `[ ]` | `[e.g., Voluntary and involuntary modeled as separate outcomes]` | accepted |
| | | | |

## Open threads

Things in progress or unresolved. Remove when closed; move outcome to decision log or session log.

- `[Thread: e.g., Whether to include stock-price change as a TVC in the Cox model or keep it only in the DiD design — leaning toward … because …]`
- `[Thread: …]`

## Known issues / gotchas

- `[e.g., Location field has a mapping break before YYYY-MM; use src/common/location_map.py]`
- `[e.g., Reason codes were re-categorized in YYYY-MM; crosswalk in docs/]`

## Questions waiting on Suki

- `[ ]`

## Last session

**Date:** `[ ]` — **Log:** `docs/sessions/[file].md`

`[3–6 bullets: what was done, what was found, what was decided. Copy the "Next actions" from the session log below.]`

## Next actions (ordered)

1. `[ ]`
2. `[ ]`
3. `[ ]`

## Exec reporting

- **Audience:** `[e.g., CPO staff, quarterly]`
- **Next deliverable:** `[what / when]`
- **Current dashboard:** `[Hex link]`
- **Canonical figures:** `[paths in outputs/ that are "the" chart for each question]`

---

## Setup checklist (delete once done)

- [ ] Fill *Data contracts* — this is the highest-leverage section for agent continuity
- [ ] Register existing models in *Model registry*
- [ ] Backfill 2–5 key past decisions into `docs/decisions/` and the *Decision log*
- [ ] Write one session log for the current state so the next agent has a starting point
- [ ] Set *Next actions*
