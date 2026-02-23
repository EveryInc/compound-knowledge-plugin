---
name: kw:work
description: Execute a knowledge work plan. Break it into tasks, do the work, and track what happened. Use after planning to actually produce the deliverables.
---

# Work

You have a plan. Now execute it. Break it into tasks, do them, track what happened.

## When to Use

* After `/kw:plan` or `/kw:review` — the plan is ready, time to execute

* "Start working on this", "Execute the plan", "Let's do this"

* When you have a clear plan and need to produce deliverables

## Process

### Step 1: Load the plan

Read the plan file. If no plan is specified:

1. Check for the most recently modified file in `plans/`
2. Ask: "Which plan should I execute? Point me to a file."

### Step 2: Break into tasks

Extract concrete deliverables from the plan. For each deliverable, create a task:

```
## Tasks

- [ ] [Task 1] — [what needs to be produced]
- [ ] [Task 2] — [what needs to be produced]
- [ ] [Task 3] — [what needs to be produced]
```

Present the task list to the user:

> "I see \[N] deliverables in this plan. Here's how I'd break them down. Want to adjust before I start?"

**Task types in knowledge work:**

| Deliverable          | How to execute                               |
| -------------------- | -------------------------------------------- |
| Strategy doc / brief | Write it using the plan as structure         |
| Email draft          | Write it, check tone, present for review     |
| Social copy          | Write variations, check against style guides |
| Data analysis        | Pull data, analyze, summarize findings       |
| Presentation         | Structure slides, write content              |
| Research synthesis   | Gather sources, extract insights, summarize  |
| Meeting agenda       | Structure topics, time-box, add context      |
| Notion page / doc    | Create and populate                          |
| Campaign assets      | Create copy, briefs, timelines               |

### Step 3: Group tasks by dependency

Before executing, sort tasks into **batches**:

```
## Execution Plan

### Batch 1 (parallel) — no dependencies
- [ ] [Task A] — independent
- [ ] [Task B] — independent

### Batch 2 (parallel) — depends on Batch 1
- [ ] [Task C] — needs output from Task A
- [ ] [Task D] — independent of C, but needs Batch 1 context

### Batch 3 (sequential) — needs user direction
- [ ] [Task E] — depends on user feedback from earlier batches
```

**Grouping rules:**

* Tasks with no dependencies on each other go in the same batch

* Tasks that need another task's output go in a later batch

* Tasks that need user feedback before starting go in their own batch

Present the execution plan to the user:

> "I've grouped these into \[N] batches. Batch 1 has \[N] independent tasks I can run in parallel. Want to adjust before I start?"

### Step 4: Execute batch by batch

**For each batch:**

1. **Announce the batch** — "Starting Batch 1: \[task names]"
2. **Launch independent tasks in parallel** — Use Task agents for tasks that don't depend on each other. For single tasks or tasks requiring heavy interaction, execute inline.
3. **Show all outputs** — Present results from the batch together
4. **Get feedback** — "Good? Or adjust before I move to Batch 2?"
5. **Mark complete** — Move to next batch

**When to parallelize within a batch:**

| Situation                                                                 | <span data-proof="authored" data-by="ai:claude">Approach</span>                       |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| 2+ independent deliverables (e.g., 3 social posts, a brief + a data pull) | <span data-proof="authored" data-by="ai:claude">Launch as parallel Task agents</span> |
| Single deliverable                                                        | Execute inline                                                                        |
| Deliverable needs back-and-forth (e.g., iterating on tone)                | Execute inline, don't delegate                                                        |

**Execution principles:**

* **Use what's available.** If there are MCP tools, APIs, or skills that can help, use them. Don't recreate what exists.

* **Follow project conventions.** Check CLAUDE.md for style guides, data sources, tool preferences.

* **Show, don't describe.** Produce the actual deliverable, not a description of what it would look like.

* **Approve between batches, not between every task.** Independent tasks don't need individual sign-off. Check in after each batch completes.

* **Fall back to sequential if unsure.** When in doubt about whether tasks are independent, run them one at a time. Wrong parallelism is worse than no parallelism.

### Step 5: Handle blockers

If you can't complete a task:

* **Missing information** — Ask the user. Be specific about what you need.

* **Missing access** — Note it and move to the next task. Come back when unblocked.

* **Scope creep** — If a task is bigger than expected, flag it: "This is turning into its own project. Should I keep going or add it as a separate plan?"

* **Quality concern** — If the output doesn't feel right, say so. "I produced this but I'm not confident about \[X]. Want to review before I continue?"

### Step 6: Track what happened

As you work, maintain a running log:

```
## Work Log

### [Task 1] ✅
- **Produced:** [what was created]
- **Location:** [file path or link]
- **Notes:** [anything notable — decisions made, things discovered]

### [Task 2] ✅
- **Produced:** [what was created]
- **Location:** [file path or link]

### [Task 3] ⏳ Blocked
- **Blocker:** [what's preventing completion]
- **Next step:** [what needs to happen]
```

### Step 7: Wrap up

When all tasks are complete (or blocked), summarize:

```
## Execution Summary

**Plan:** [plan name]
**Tasks completed:** [N] of [total]
**Deliverables produced:**
- [deliverable 1] — [location]
- [deliverable 2] — [location]

**Still open:**
- [blocked task] — [blocker]

**Discoveries:**
- [anything learned during execution worth noting]
```

### Step 8: Offer next steps

Use AskUserQuestion:

**Question:** "Execution complete. \[N] deliverables produced. What next?"

**Options:**

1. **Run** **`/kw:review`** — Quality check the outputs
2. **Run** **`/kw:compound`** — Save learnings from this session
3. **Continue working** — Pick up blocked tasks or add new ones
4. **Ship it** — Done, move on

## Important Rules

* **Produce, don't plan.** This is execution mode. If you find yourself writing another plan, you're in the wrong workflow. Use `/kw:plan` for that.

* **Show your work.** After each task, show the actual output. Don't say "I would create a doc that..." — create the doc.

* **Respect scope.** The plan defines what to do. If something isn't in the plan, ask before adding it. Scope creep is the enemy of finishing.

* **Track everything.** The work log is how you know what happened. It also feeds `/kw:compound` with concrete results to learn from.

* **Ask for feedback between batches.** Knowledge work is subjective. Check in after each batch rather than producing everything and hoping it's right. Independent tasks within a batch don't need individual sign-off.