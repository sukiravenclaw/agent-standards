# Playbook — agent-continuous repos

Assumes the one-time install is done: `~/GitHub/agent-standards/` exists with `CLAUDE.md`, `commands/`, `templates/`, and is symlinked from `~/.claude/CLAUDE.md` and `~/.claude/commands/`.

---

## A. Picking up work in an already set-up repo

```bash
cd ~/GitHub/<repo>
claude
```

Then, as your first message:

```
/open-session
```

or, if you already know today's goal:

```
/open-session <goal in one line>
```

e.g. `/open-session add stock-price change as a lagged TVC to the Cox model and compare c-index against D-03`

The agent reads `AGENTS.md`, `STATE.md`, the latest session log, and checks git for drift, then reports where things stand and proposes a first step. Reply with one of:

- `go` — do the proposed first step
- `go, then <next thing>` — chain tasks
- `skip that, do <new task> instead` — it will note the divergence from *Next actions* in the session log
- `answers: <answers to [UNKNOWN] items>` — fills data contracts before starting

Mid-session, give tasks normally. When done — **every time**, even for ten-minute sessions:

```
/close-session
```

Optional notes as an argument: `/close-session Suki decided to drop the location segment for Q3 reporting`.

**Fallback if commands aren't loaded** (e.g., a different tool, or `/memory` doesn't show the global file): paste this instead of `/open-session`:

> Read `AGENTS.md`, then `STATE.md` in full, then the newest file in `docs/sessions/`. Check `git log` for anything newer than that log. Summarize in one paragraph where the work stands, list the data contracts in force, flag any contradiction between the three sources, and propose the first step from *Next actions*. Don't start until I confirm.

---

## B. Setting up a brand-new repo

```bash
mkdir -p ~/GitHub/<repo> && cd ~/GitHub/<repo>
git init
claude
```

Then:

```
/init-repo <one line: what this repo answers and for whom>
```

e.g. `/init-repo Forecast quarterly headcount by org from hiring plan + attrition hazard, for Finance planning`

The agent scaffolds the files from `templates/`, asks you ~6 questions in one message, fills `AGENTS.md`/`STATE.md`/`README.md`, writes a baseline session log, and commits. Answer the questions, review the `[UNKNOWN]` list it returns, then:

```
/open-session
```

and start working.

**For an existing repo that predates this setup** (code and history already there), the same `/init-repo` command detects that and runs the audit first, pausing to show you `docs/_audit_<date>.md` before it fills anything in. For a large or messy repo, use the longer `claude-code-setup-prompt.md` instead — it's the same process with more explicit phases and checkpoints.

---

## C. Keeping it healthy

- `/memory` — confirm what's loaded whenever behavior seems off.
- Repeated corrections → global file (`~/GitHub/agent-standards/CLAUDE.md`), commit, push.
- Repo-specific lessons → `AGENTS.md` → *Gotchas* (via `/close-session` step 5).
- Quarterly: from `~/GitHub`, ask Claude Code to read all `docs/sessions/` across repos and propose global-file consolidations and deletions.
