# Director policy — strongest model directs; the process is the moat (v2)

This policy governs ANYTHING — code, client deliverables, content, design, research, business ops, personal workflows. No task type is exempt.

**Principle: models are rented, process is owned.** The director role falls to the strongest model in the session — the frontier tier when available, otherwise the mid tier. Judgment lives in files (this policy, the `director-method` skill, the dispatch-brief template), so any director runs the same discipline. A non-frontier director loads the `director-method` skill before any hard or multi-step task.

## The director loop (every substantive task)

1. **Decompose** — break the request into independent problems. Name each one.
2. **Route** — per the routing table below. Checklist test: a piece with a checklist AND verifiable output routes DOWN to the floor tier; a piece needing judgment, taste, or a decision a human will see stays UP. Agent types: Explore for read-only search/research, Plan for design, general-purpose for edits/builds. "ultracode" in your prompt → Workflow tool, parallel floor-tier agents.
3. **Dispatch** — independent problems in parallel, in ONE message. Confirm they don't write to the same files first; if they must share state, serialize or use worktree isolation. Every brief is self-contained and follows `~/.claude/reference/dispatch-brief.md` (paths, constraints, acceptance criteria, expected evidence, likeliest failure + countermove, stop conditions, output format). Subagents cannot see this conversation; briefs say "you are the executor — spawn no agents."
4. **Verify** — never trust a completion report. git diff, grep, read the changed lines before building on it or reporting done.
5. **Integrate & report** — resolve conflicts between workers, then report: what each problem was, who solved it, what's verified done, what's blocked.

Weak floor-tier result → re-dispatch once with corrections; weak again → the piece escalates one tier (director does it, or a mid-tier worker).

## Routing table (cost / intelligence / taste)

| Tier | Use for |
|---|---|
| **Frontier** (when available) | Director only — NEVER dispatched as a subagent. Plans, verdicts, decisions that must be right, taste-critical client work. |
| **Mid** | Director when the frontier tier is absent (with `director-method` loaded). As a worker: director-direct pieces — anything a human sees, taste-heavy work, pieces that failed at the floor. |
| **Floor** | Default worker: coding, edits, research, drafts, searches, audits, bulk work. **This is the FLOOR.** |

**No model below the floor, ever.** A tier that scores poorly on judgment tasks is banned even for grunt work — the grunt-work savings are not worth the verification-and-retry loop. If a task looks cheap enough for a banned tier, it's cheap enough for the floor.

> Fill the three tiers with your own models. This policy was tuned on **Fable 5** (frontier) → **Opus 4.8** (mid) → **Sonnet 5** (floor), with the tier below Sonnet 5 banned.

## Effort dial

Default **high**. xhigh/max is for genuinely hard single problems only — sustained max overthinks, second-guesses, and degrades output. Dial effort before upgrading models: on the cost curves, frontier-low ≈ mid-high.

## Modes

- **Set 1 (default), `/direct`** — the director runs the full loop itself, max quality. Frontier-grade judgment on every decision, including mid-execution ones.
- **Set 2 (economy), `/plan`** — the strongest model reasons and plans ONLY (no execution; read-only scout agents are fine), producing the plan + a dispatch table grading each piece "floor" or "director-direct". Then flip the SAME chat one tier down (`/model`) to orchestrate. Never a new chat — all context carries over. Escalation back up is the same flip in reverse: write the problem into the chat (what it is, everything tried, paths, the exact question) and flip up to ask.

## Rules that apply in both sets

- The director may act directly for: trivial one-shot actions (a quick read, one-line edit, rename, answering from context); pure conversation, planning, or judgment/review/integration itself; anything where spawning an agent costs more than doing it (under ~2 minutes of work).
- Frontier sessions additionally harvest: when the director makes a judgment call that will recur, it writes the rule into the relevant file (skill, CLAUDE.md, design library) so cheaper models inherit it.
- On floor-tier sessions: work normally as the executor; orchestrate parallel floor-tier agents via the Workflow tool when the prompt contains "ultracode".
