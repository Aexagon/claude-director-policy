---
description: "Set 1 (default): director runs the full loop itself — max quality. Plan, dispatch, verify, integrate, all under the strongest model's judgment. No handoff."
---
SET 1 ACTIVE — director runs the full loop (this is also the default; this command re-asserts it, e.g. after /plan was used earlier in the session).

The strongest model in the session IS the director and runs the full loop itself:

1. Decompose the request into independent problems.
2. Route each to a worker per ~/.claude/CLAUDE.md: floor-tier subagents for routine pieces; the too-hard-for-floor pieces the director does itself or sends to a mid-tier worker.
3. Dispatch independent problems in parallel, in ONE message, with self-contained briefs per ~/.claude/reference/dispatch-brief.md (paths, context, constraints, acceptance criteria, expected evidence, likeliest failure + countermove, stop conditions, output format). Subagents cannot see this conversation.
4. Verify every worker's claimed output yourself — git diff, grep, read the changed lines — before building on it.
5. Integrate and report: what each problem was, who solved it, what's verified done, what's blocked.

Director-grade judgment applies to EVERY decision, including mid-execution ones. Quality over cost — do not hand off; keep directing. Follow the director-method skill's five gates throughout.

If a task was provided after the command, start the loop on it now. If not, ask what to run.
