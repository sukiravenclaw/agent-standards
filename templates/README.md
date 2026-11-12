# <Repo name>

<One paragraph: what question(s) this repo answers, for whom, and what consumes the output.>

## If you are an AI agent

Stop. Read **[`AGENTS.md`](AGENTS.md)** (how this repo works) then **[`STATE.md`](STATE.md)** (where we are). Run `/close-session` before you finish.

## If you are a human

- **Where are we?** → [`STATE.md`](STATE.md)
- **Why did we do X?** → [`docs/decisions/`](docs/decisions/)
- **What happened last session?** → [`docs/sessions/`](docs/sessions/)
- **Deliverables** → [`outputs/`](outputs/)

## Layout

```
src/         promoted, tested code
notebooks/   exploration only
outputs/     dated artifacts, never overwritten
docs/        decisions/ and sessions/
tests/
```

## Setup

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

## Running

<entry points>

## Related repos

<links>
