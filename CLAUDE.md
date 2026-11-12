# Global agent instructions — Suki

> Lives at `~/.claude/CLAUDE.md`. Loads automatically in every Claude Code session, every repo.
> Per-repo context lives in that repo's `AGENTS.md` (durable) and `STATE.md` (living).
> Precedence: repo `AGENTS.md` overrides this file where they conflict; repo `STATE.md` is the source of truth for "where are we."

---

## 1. Who you are working with

- **Suki** — Staff Data Scientist, Roblox. Built and leads the People Analytics function.
- PhD in Quantitative Psychology. Deep in psychometrics, IRT, MFRM, causal inference (DiD, IV, BSTS, synthetic control, PSM), survival analysis, network science.
- Also teaches at USC Annenberg (fall) and works on AI-evaluation and LLM-as-judge projects.
- **Calibrate accordingly:** assume expert statistical literacy. Don't explain standard methods; explain *why this method here*. She will check your assumptions — state them. Prefer defensible measurement over clever modeling. Propose the pragmatic path, then flag the rigorous alternative and its cost.

## 2. Universal methodological rules

Apply in every analytical repo unless the repo's `AGENTS.md` records an explicit exception.

1. **Prediction ≠ explanation.** Feature importance / SHAP is association. Causal language requires a design and a stated identifying assumption.
2. **No leakage.** Before reporting any model result, check for fields populated because of the outcome, and for covariates measured at or after the outcome window.
3. **Every estimate carries uncertainty and n.** Point estimates without intervals don't ship. Name the interval method.
4. **Minimum cell sizes are enforced** for any segment-level people data. The threshold lives in the repo's `STATE.md` → *Data contracts*.
5. **Reproducibility.** Every reported number traces to code + a data snapshot ID. No hand-edited numbers. Notebooks are scratch; load-bearing logic gets promoted to `src/`.
6. **Constructs without natural units** (collaboration quality, meeting effectiveness, output quality) must state how they're validated before they're used as inputs or outcomes.
7. **Don't expand scope silently.** If something might be out of scope for the repo, ask.

## 3. Standard repo layout

Every analytical repo follows this shape. The repo's `AGENTS.md` records deviations.

```
<repo>/
├── CLAUDE.md          ← contains `@AGENTS.md`; may also import STATE.md
├── AGENTS.md          ← repo-specific: scope, rules/exceptions, layout, gotchas
├── STATE.md           ← living state; updated every session
├── README.md          ← human-facing overview + setup
├── data/              ← never committed
├── src/               ← promoted, tested code; subpackages by workstream
├── notebooks/         ← exploration only
├── outputs/           ← dated subfolders YYYY-MM-DD_<topic>/, never overwritten
├── docs/decisions/    ← one file per decision (§6)
├── docs/sessions/     ← one file per session (§7)
└── tests/
```

## 4. Session protocol

**Start** — run `/open-session`, or manually: read `AGENTS.md`, then `STATE.md` fully, then the latest `docs/sessions/` file. Confirm your understanding of the current task in one paragraph before touching code. If `STATE.md` looks stale or contradictory, say so.

**During** — work `STATE.md` → *Next actions* in order unless told otherwise. Write decision records at the moment a non-trivial choice is made, not at the end.

**End (mandatory, even for short sessions)** — run `/close-session`, or manually:
1. Write `docs/sessions/YYYY-MM-DD_<topic>.md` (§7).
2. Update `STATE.md`: *Last session*, *Next actions*, *Open threads*, *Known issues*, any changed data contracts.
3. Ensure any decision has a record in `docs/decisions/` and a row in `STATE.md` → *Decision log*.
4. Report in ≤5 bullets: what changed, what to do next.

Skipping the close-out is the single biggest cause of lost context. Don't.

## 5. Working style

- Python by default; follow the style already in the repo. Don't introduce a new framework without a decision record.
- Config in one place. No hardcoded dates, paths, thresholds.
- Don't re-derive definitions that exist in `STATE.md` → *Data contracts*. Use them.
- Don't vendor code from sibling repos; link to them.
- Documentation-only tasks must not touch code, data, or outputs.
- Don't invent facts about the repo or its history. Mark unknowns and ask.

## 6. Decision record template — `docs/decisions/NNNN_<slug>.md`

```
# NNNN — <Decision title>
Date:
Status: proposed | accepted | superseded by NNNN
Context: what question forced this choice
Options considered: (2–4, one line each, with trade-off)
Decision:
Consequences: what this constrains or enables
Evidence: notebooks/outputs/commits that informed it
```

## 7. Session log template — `docs/sessions/YYYY-MM-DD_<topic>.md`

```
# Session — YYYY-MM-DD — <topic>
Goal:
What was done: (bullets; files and commits)
Results: (numbers with intervals; link outputs)
Decisions made: (link records)
Dead ends: (what didn't work and why)
Open questions for Suki:
Next actions: (mirror into STATE.md)
```

## 8. Communication

- Answer first, then evidence, then caveats.
- Numbers always carry uncertainty and sample size.
- Exec-facing artifacts: plain language, one chart per idea, methods in an appendix.
- Distinguish *evidenced* (cite file/commit) from *inferred*.

## 9. Domain glossary — Workday/engagement survey items

Confirmed by Suki (2026-09-01). These question codes recur across repos that touch
survey/engagement data (columns like `survey_last1_QID*`, `survey_last2_QID*`):

- **QID3** — manager recommendation score (would you recommend your manager)
- **QID5_3** — intent to stay
- **QID6** — company satisfaction / eSAT

If a repo's own data dictionary defines these differently, trust the repo — flag the
conflict to Suki rather than silently overriding with this list.
