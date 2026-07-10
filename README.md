# Claude Director Policy

A portable operating discipline for [Claude Code](https://claude.com/claude-code): the **strongest model in the session directs** the work — decomposing it, routing each piece, and verifying results — while cheaper models do the execution. The judgment lives in these files, not in any one model, so the same process runs whether your director is a frontier model or a step down.

> **Principle: models are rented, process is owned.**

## Why

A single top-tier model doing everything gives the best quality *per unit of work* — but it doesn't scale: no parallelism, context rot on long tasks, and premium rates on grunt work. Delegation fixes all three, but only if the delegation is disciplined. This repo encodes that discipline as files a model reads and follows:

| File | What it is |
|---|---|
| **`CLAUDE.md`** | The director policy — the loop, the routing table, the two modes. |
| **`skills/director-method/SKILL.md`** | "The Director Method" — five gates any model runs to scope, gather evidence, attack its own plan, verify, and report. |
| **`commands/direct.md`**, **`commands/plan.md`** | The two operating modes, as slash commands. |
| **`reference/dispatch-brief.md`** | The self-contained brief every delegated task must fill out. |

## The two modes

| Command | Mode | What happens |
|---|---|---|
| `/direct` *(default)* | Director runs the full loop | The strongest model plans, dispatches workers, verifies every result, and integrates — top-tier judgment on **every** decision, including the mid-execution ones. Max quality. |
| `/plan` *(economy)* | Director plans only | The strongest model reasons and produces a plan + a dispatch table, then you flip the same chat one tier down to orchestrate. Cheaper: you trade a little mid-execution judgment for roughly half the orchestration cost. |

Both stay in **one chat** — you switch models with `/model` and the context carries over. No new chats, no copy-paste.

## The routing table

| Tier | Role |
|---|---|
| **Frontier** *(director)* | Plans, verdicts, decisions that must be right, taste-critical work. **Never** dispatched as a subagent. |
| **Mid** *(worker + fallback director)* | Anything a human sees, taste-heavy work, pieces that failed at the floor. Directs when no frontier model is in the session. |
| **Floor** *(worker)* | Coding, edits, research, drafts, searches, audits, bulk work. **This is the floor — nothing below it runs.** |

The repo names the specific models this was tuned on (Fable 5 → Opus 4.8 → Sonnet 5, with the tier below the floor banned). Swap them for your own three tiers.

## The five gates (the heart of it)

1. **Scope before work** — restate the task + win condition; name what's out of scope.
2. **Evidence before reasoning** — never design from memory; open the file, quote the line.
3. **Attack your own answer** — try to kill it before shipping; name the failure mode + countermove.
4. **Verify before declaring done** — "it ran" ≠ "it's right"; never trust a completion report.
5. **Report with calibration** — lead with the outcome; separate verified / inferred / assumed.

Full text: [`skills/director-method/SKILL.md`](skills/director-method/SKILL.md).

## Install

Copy into your Claude Code config (`~/.claude`). Review `CLAUDE.md` first — merge it into your existing one rather than overwriting if you already have global instructions.

```bash
cp CLAUDE.md ~/.claude/CLAUDE.md
mkdir -p ~/.claude/commands ~/.claude/skills ~/.claude/reference
cp commands/*.md ~/.claude/commands/
cp -r skills/director-method ~/.claude/skills/
cp reference/dispatch-brief.md ~/.claude/reference/
```

Then, optionally, set your default model and effort in `~/.claude/settings.json` (for example, default to your frontier model at `high` effort so every session opens as a director).

## License

[MIT](LICENSE). Adapt it freely — that's the point.
