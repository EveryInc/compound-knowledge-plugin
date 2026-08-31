---
name: kw:lfg
description: "Run the full Compound Knowledge loop end-to-end, hands-off with no check-ins between stages. Use only when the user explicitly asks to ship the rest of the knowledge-work loop autonomously (plan → review → work → compound), or invokes /kw:lfg directly. Not for in-the-loop work where the user reviews each stage — use /kw:plan, /kw:review, /kw:work, or /kw:compound instead."
argument-hint: "[topic | brainstorm path | plan path | plan:<path>]"
---

<lfg_request> #$ARGUMENTS </lfg_request>

# LFG (Knowledge Work)

Run the Compound Knowledge loop autonomously: **plan → review → work → compound**. No stage-handoff menus. Narrate progress; do not stop to ask which stage is next.

This is the knowledge-work counterpart to Compound Engineering's `/lfg`. CE ships code to an open PR; CK ships knowledge deliverables and compounds learnings into `docs/knowledge/`.

CRITICAL: Execute every step below **in order**. Do not jump ahead to `/kw:work` before a plan exists (unless a plan path was provided). Do not ask "what next?" between stages.

Resolve every skill named below against the host's available-skills list and invoke that exact entry (hosts may namespace it, e.g. `compound-knowledge:kw-plan`).

## When to Use

* User says "just run the loop", "lfg", "ship the rest", or picks **Ship the rest with `/kw:lfg`** from a brainstorm/plan handoff
* Direction is clear enough that mid-loop steering is optional
* **Not** for exploratory brainstorming — finish `/kw:brainstorm` interactively first, then LFG

## Inputs

Parse `$ARGUMENTS` in this order:

| Form | Meaning |
|------|---------|
| `plan:<path>` | Skip Step 1. Use this plan; start at review. |
| Existing file under `plans/` matching `brainstorm-*.md` | Origin doc for planning. |
| Existing file under `plans/` that is **not** a brainstorm (e.g. `plans/strategy-….md`) | Treat as an existing plan — skip Step 1; start at review (same as `plan:`). |
| Free-text topic | Plan from the topic (and any prior conversation context). |
| Empty | Use the most recent brainstorm in `plans/`, else the most recent non-brainstorm plan, else the active conversation topic. If none exist, STOP and tell the user what to pass. |

If a path looks like a plan file but does not exist, STOP and report — do not invent a plan silently.

## Stage narration

Before each step, one line:

```
**LFG → Stage: [Plan|Review|Work|Compound]** — [what this step should produce]
```

After each step, one line naming what it produced (plan path, P1 count, deliverable count, knowledge files).

## Pipeline contract

When invoking child skills, pass **`mode:pipeline`** in the invocation arguments (plus the plan/brainstorm path or topic). That carrier is the durable signal — do **not** rely on `disable-model-invocation` (that is skill frontmatter for blocking invocation, not a runtime mode).

Child skills under `mode:pipeline` must:

* Skip AskUserQuestion and interactive waits
* Write files without waiting
* **Return structured results only** — they must **not** load the next `/kw:*` skill themselves
* Still follow non-interactive Important Rules (cite sources, write execution logs, quality filters)

LFG alone advances stages after each child returns.

---

## Step 1: Plan

**Skip** if a plan path was resolved from inputs (`plan:` or existing non-brainstorm `plans/*.md`).

1. Invoke `kw:plan` with `mode:pipeline` on the brainstorm path or topic.
2. GATE: STOP if no plan file was written. Report why and halt.
3. **Record `plan_path`** for later steps.

## Step 2: Review

1. Invoke `kw:review` with `mode:pipeline` on `plan_path`.
2. If **P1** findings exist:
   - Attempt a single auto-fix pass on the plan (and any attached brief) addressing each P1
   - Re-run `kw:review` once with `mode:pipeline`
   - If P1s remain: GATE STOP. Report remaining P1s and `plan_path`. Do not execute a plan with unresolved critical findings unless the user later overrides interactively.
3. P2/P3 findings: note them in narration; continue (apply obvious safe P2 fixes when cheap; otherwise leave for compound/residuals).

## Step 3: Work

1. Invoke `kw:work` with `mode:pipeline` on `plan_path`.
2. Child skips per-batch approval prompts; still writes the **Execution Log** into the plan file after each batch.
3. GATE: STOP if zero deliverables were produced and work is blocked on missing access/info the agent cannot resolve. Report blockers and `plan_path`.
4. **Record deliverable paths** for the close-out.

## Step 4: Compound

1. Invoke `kw:compound` with `mode:pipeline` against this session (plan + execution log + deliverables).
2. Pipeline compound auto-approves **1–3** high-signal learnings after duplicate + stale checks; skips weak ones rather than saving noise.
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

Terminal artifacts are **deliverables + compounded knowledge** — not a git PR/CI green. If the project wants commits or a PR, the user (or Compound Engineering `/lfg`) owns that separately.

---

## Important Rules

* **Hands-off between stages.** The whole point is not asking "plan or work next?" after brainstorm. Interactive steering belongs in the individual `/kw:*` skills.
* **Plan before work.** Never invent an execution path without a written plan file (unless a plan path was provided).
* **P1 is a hard gate.** Wrong strategy or wrong data must not silently ship.
* **Compound closes the loop.** Skipping Step 4 means the next cycle cannot benefit — only skip when Step 3 produced nothing meaningful.
* **Brainstorm stays interactive.** LFG does not replace `/kw:brainstorm`; it consumes its output (or a topic) and runs the rest.
* **LFG owns the chain.** Children in `mode:pipeline` return to LFG; they do not self-chain.

## Relationship to Compound Engineering `/lfg`

| | CE `/lfg` | CK `/kw:lfg` |
|--|-----------|--------------|
| Domain | Software | Knowledge work |
| Core pipeline | plan → work → simplify → code-review → PR → CI | plan → review → work → compound |
| Terminal artifact | Open PR (often CI-green) | Deliverables + `docs/knowledge/` entries |
| Typical entry | Feature description or requirements plan | Brainstorm origin doc, topic, or existing plan |
| Runtime carrier | `mode:pipeline` / return-to-caller | `mode:pipeline` on each child invoke |
