---
name: kw:confidence
description: Gut-check what you know and don't know before proceeding. Use at any point to assess confidence, surface gaps, and decide whether to proceed or dig deeper.
---

# Confidence

Pause and honestly say what you're confident about and what you're not — like a colleague would. Then decide whether to proceed or dig deeper.

## When to Use

* Before committing to a plan or starting execution

* When something feels uncertain but you can't pinpoint what

* After research, to verify you have enough to proceed

* As a gut-check during any `/kw:` workflow

## Process

### Step 1: Identify what's being assessed

Scan the conversation for the active task, plan, or workflow:

* If mid-`/kw:work` — assess the current or next task
* If mid-`/kw:plan` — assess the plan being structured
* If a plan file exists — read it and assess the approach
* If the user gave context — assess what they described

If there's nothing to assess (empty session, no context):

> "What should I assess? Describe what you're working on or point me to a file."

### Step 2: Assess honestly

Think through these areas internally — but don't output them as a checklist:

* **Task understanding** — Do I know exactly what's being asked?
* **Information sufficiency** — Do I have what I need to do this well?
* **Approach certainty** — Is this approach proven or am I guessing?
* **Risk awareness** — Can I see what could go wrong?

**Rules for honest assessment:**

* Assess each area independently. Don't let confidence in one area inflate another.
* Be specific — name files, numbers, assumptions, and unknowns.
* Don't hedge on things you're genuinely confident about. If you've read the files and the approach is proven, say so.
* Don't fake confidence on things you're not sure about. If your knowledge came from a quick search rather than deep familiarity, say that.

### Step 3: Produce the confidence check

Write in plain prose with this structure:

```
## Confidence Check

**Confident about:** [What you know and why. Be specific — name the files
you've read, the patterns you recognize, the experience you're drawing on.
This can be a sentence or a short paragraph.]

**Less confident about:** [What you don't know and why it matters. Name the
specific gaps — missing data, unverified assumptions, unfamiliar territory.
Explain what could go wrong if these gaps aren't addressed.]

**My recommendation:** [One of three paths:
- "Proceed." — confidence is high, no meaningful gaps
- "Proceed, but [caveat]." — mostly confident, one area to watch
- "Pause for [specific thing]." — a gap needs resolving first]
```

**If everything is high confidence**, keep it short:

> **High confidence.** Task is clear, I've read the relevant files, the approach matches established patterns. No gaps I can identify. Ready to proceed.

Don't force a full breakdown when there's nothing to break down. Two sentences is fine.

### Step 4: Offer next steps

Use AskUserQuestion:

**Question:** "What would you like to do?"

**Options:**

1. **Proceed** — Continue with current approach
2. **Increase confidence** — Show specific actions to resolve the gaps
3. **Run `/kw:plan`** — Structure a plan if one doesn't exist yet
4. **Save assessment** — Write to the active plan file or `plans/confidence-{date}.md`

**If the user selects "Increase confidence":**

Produce a ranked list of specific, executable actions. Rank by impact — biggest confidence gain first:

```
## To Increase Confidence

1. [What to do] — [Why it matters. What gap it closes.]

2. [What to do] — [Why it matters. What gap it closes.]

3. [What to do — note if it needs user input] — [Why it matters.]

Want me to start with #1?
```

Each action must be specific enough to execute immediately. "Read `data/q4-results.csv` to confirm the $50K benchmark" not "gather more data." Note which actions Claude can do autonomously vs. which need user input.

Use AskUserQuestion:

**Question:** "How would you like to proceed?"

**Options:**

1. **Start with #1** — Execute the top-ranked action
2. **Pick a different action** — Choose which to tackle first
3. **Proceed anyway** — Accept current confidence level and continue

After executing action(s), reference the improvement conversationally:

> "That Q4 data confirms the $50K target is realistic — that was the main gap. Confidence is higher now."

Then return to Step 4 to offer next steps again.

**If the user selects "Proceed" and a workflow is active:**

Explicitly re-anchor to the interrupted workflow:

> "Resuming `/kw:work` at Task 3."

Then continue where you left off. The confidence check is a non-destructive interrupt.

## Important Rules

* **Never give a number.** No percentages, no 1-10 scales, no letter grades. Write in prose.

* **Be specific.** "Missing Q4 data" not "some information gaps." Name files, assumptions, unknowns.

* **Don't hedge on what you know.** Confidence theater — hedging on everything to seem careful — is worse than overconfidence. If you've done the work, say so clearly.

* **Actions must be executable.** Every item in the "increase confidence" list must be something you or the user can do right now. "Read file X" not "gather more data."

* **Non-destructive interrupt.** If invoked mid-workflow, resume exactly where you left off after. Don't restart the parent workflow.

* **Keep it proportional.** High confidence = 2 sentences. Mixed confidence = a few short paragraphs. Never a wall of text.

* **This is not `/kw:review`.** Confidence assesses what *you* know and don't know — your epistemic state. Review assesses whether a *finished artifact* is good enough. They're complementary, not alternatives.

## Pipeline Mode

When invoked with `disable-model-invocation` context (e.g., from an orchestrator or automation):

- Skip all AskUserQuestion prompts
- Use sensible defaults for all choices
- Write output files without waiting for confirmation
- Proceed to the next suggested skill automatically
- Output structured results that the calling context can parse
