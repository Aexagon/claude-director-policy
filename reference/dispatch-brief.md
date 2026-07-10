# Dispatch brief template

Every subagent brief is self-contained — the worker cannot see the conversation. Fill every field; a field you can't fill means the piece isn't ready to dispatch.

```
ROLE
You are the executor. Spawn no agents. Do the work yourself.

TASK
<one line: what to produce/change, and where>

CONTEXT
<absolute paths to every file involved; relevant constraints from the
conversation, restated — style rules, banned moves, prior decisions>

CONSTRAINTS
<hard limits: what must not change, what must not be touched,
style/brand rules that apply>

ACCEPTANCE CRITERIA
<checklist — each item independently checkable by the director>

EXPECTED EVIDENCE
<per step: what you should see if it worked — the passing test, the
diff shape, the rendered output, the matching number>

LIKELIEST FAILURE + COUNTERMOVE
<the most probable way this goes wrong, its early signals, and what
to do instead when you see them>

STOP CONDITIONS
<the situations where you STOP and report rather than improvise —
missing file, failing assumption, scope fork, anything destructive>

OUTPUT FORMAT
<exactly what to return: files written + paths, plus a report that
separates verified facts / inferences / assumptions, and flags
anything not verified>
```

## Director-side rules

- Route by the checklist test: checklist + verifiable output → floor tier; judgment, taste, or human-visible decisions → stay up. The floor is the floor; the tier below it is banned.
- Parallel dispatch only for pieces that don't write to the same files.
- Verify every claim in the worker's report against the actual files before integrating (Gate 4 of director-method).
- Weak result → re-dispatch once with corrections; weak again → escalate the piece one tier.
