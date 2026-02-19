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

### Step 3: Execute task by task

For each task:

1. **Mark in progress** — Announce what you're working on
2. **Do the work** — Produce the deliverable using available tools
3. **Show the output** — Present what you made
4. **Get feedback** — "Good? Or adjust?"
5. **Mark complete** — Move to next task

**Execution principles:**

* **Use what's available.** If there are MCP tools, APIs, or skills that can help, use them. Don't recreate what exists.

* **Follow project conventions.** Check CLAUDE.md for style guides, data sources, tool preferences.

* **Show, don't describe.** Produce the actual deliverable, not a description of what it would look like.

* **One task at a time.** Don't try to do everything in parallel. Knowledge work benefits from sequential focus.

* **Check in after each task.** The user may want to adjust direction based on what they see.

### Step 4: Handle blockers

If you can't complete a task:

* **Missing information** — Ask the user. Be specific about what you need.

* **Missing access** — Note it and move to the next task. Come back when unblocked.

* **Scope creep** — If a task is bigger than expected, flag it: "This is turning into its own project. Should I keep going or add it as a separate plan?"

* **Quality concern** — If the output doesn't feel right, say so. "I produced this but I'm not confident about \[X]. Want to review before I continue?"

### Step 5: Track what happened

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

### Step 6: Wrap up

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

### Step 7: Offer next steps

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

* **Ask for feedback often.** Knowledge work is subjective. Check in after each deliverable rather than producing everything and hoping it's right.