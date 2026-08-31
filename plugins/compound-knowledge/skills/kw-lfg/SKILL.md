---
name: kw:lfg
description: "Run the full Compound Knowledge loop end-to-end, hands-off with no check-ins between stages. Use only when the user explicitly asks to ship the knowledge-work loop autonomously (plan → review → work → compound), or invokes /kw:lfg directly. Not for in-the-loop work where the user reviews each stage — use /kw:plan, /kw:review, /kw:work, or /kw:compound instead."
argument-hint: "[topic, brainstorm path, or plan:<path> to skip planning]"
---

<lfg_request> #$ARGUMENTS </lfg_request>

# LFG (Knowledge Work)

Run the Compound Knowledge loop autonomously: **plan → review → work → compound**. No stage-handoff menus. Narrate progress; do not stop to ask which stage is next.

This is the knowledge-work counterpart to Compound Engineering's `/lfg`. CE ships code to an open PR; CK ships knowledge deliverables and compounds learnings into `docs/knowledge/`.

CRITICAL: Execute every step below **in order**. Do not jump ahead to `/kw:work` before a plan exists (unless invoked with `plan:<path>`). Do not ask "what next?" between stages.

Resolve every skill named below against the host's available-skills list and invoke that exact entry (hosts may namespace it, e.g. `compound-knowledge:kw-plan`).

## When to Use

* User says "just run the loop", "lfg", "ship it", or picks **Ship the loop with `/kw:lfg`** from a brainstorm/plan handoff
* Direction is clear enough that mid-loop steering is optional
* **Not** for exploratory brainstorming — finish `/kw:brainstorm` interactively first, then LFG

## Inputs

Parse `$ARGUMENTS`:

| Form | Meaning |
|------|---------|
| `plan:plans/...md` or `plan:<path>` | Skip Step 1. Use this plan; start at review. |
| Path to `plans/brainstorm-*.md` | Origin doc for planning. |
| Free-text topic | Plan from the topic (and any prior conversation context). |
| Empty | Use the most recent brainstorm in `plans/`, else the active conversation topic. If neither exists, STOP and tell the user what to pass. |

## Stage narration

Before each step, one line:

```
**LFG → Stage: [Plan|Review|Work|Compound]** — [what this step should produce]
```

After each step, one line naming what it produced (plan path, P1 count, deliverable count, knowledge files).

## Pipeline contract

When invoking child skills, run them in **Pipeline Mode**:

* Pass context equivalent to `disable-model-invocation` / pipeline so they skip AskUserQuestion
* Use sensible defaults; write files without waiting
* Do **not** present their interactive handoff menus — LFG owns progression
* Child skills still follow their Important Rules (cite sources, write execution logs, etc.)

---

## Step 1: Plan

**Skip** if invoked with `plan:<path>` and that file exists.

1. Invoke `kw:plan` on the brainstorm path or topic.
2. GATE: STOP if no plan file was written. Report why and halt.
3. **Record `plan_path`** for later steps.

## Step 2: Review

1. Invoke `kw:review` on `plan_path`.
2. If **P1** findings exist:
   - Attempt a single auto-fix pass on the plan (and any attached brief) addressing each P1
   - Re-run `kw:review` once
   - If P1s remain: GATE STOP. Report remaining P1s and `plan_path`. Do not execute a plan with unresolved critical findings unless the user later overrides interactively.
3. P2/P3 findings: note them in narration; continue (apply obvious safe P2 fixes when cheap; otherwise leave for compound/residuals).

## Step 3: Work

1. Invoke `kw:work` on `plan_path`.
2. In pipeline mode: skip per-batch approval prompts; still write the **Execution Log** into the plan file after each batch.
3. GATE: STOP if zero deliverables were produced and work is blocked on missing access/info the agent cannot resolve. Report blockers and `plan_path`.
4. **Record deliverable paths** for the close-out.

## Step 4: Compound

1. Invoke `kw:compound` against this session (plan + execution log + deliverables).
2. In pipeline mode: auto-approve **1–3** high-signal learnings; skip weak ones rather than saving noise. Still run duplicate + stale checks before write.
3. Record saved `docs/knowledge/` paths (or explicitly "nothing worth saving").

## Step 5: DONE

Output a self-contained recap:

```
<promise>DONE</promise>

**LFG complete.**

Plan: [plan_path]
Deliverables:
- [path or title]
Learnings:
- [docs/knowledge/... | none]

Residuals / watch-outs:
- [remaining P2s, blockers, or assumptions]
```

Do not open a PR or push git remotes — knowledge work ends at deliverables + compounded knowledge. If the project wants git commits, the user (or a separate CE `/lfg`) owns that.

---

## Important Rules

* **Hands-off between stages.** The whole point is not asking "plan or work next?" after brainstorm. Interactive steering belongs in the individual `/kw:*` skills.
* **Plan before work.** Never invent an execution path without a written plan file (unless `plan:` was provided).
* **P1 is a hard gate.** Wrong strategy or wrong data must not silently ship.
* **Compound closes the loop.** Skipping Step 4 means the next cycle cannot benefit — only skip when Step 3 produced nothing meaningful.
* **Brainstorm stays interactive.** LFG does not replace `/kw:brainstorm`; it consumes its output (or a topic) and runs the rest.

## Relationship to Compound Engineering `/lfg`

| | CE `/lfg` | CK `/kw:lfg` |
|--|-----------|--------------|
| Domain | Software | Knowledge work |
| Core pipeline | plan → work → simplify → code-review → PR → CI | plan → review → work → compound |
| Terminal artifact | Open PR (often CI-green) | Deliverables + `docs/knowledge/` entries |
| Typical entry | Feature description or requirements plan | Brainstorm origin doc, topic, or existing plan |
