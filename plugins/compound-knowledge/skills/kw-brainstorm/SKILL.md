---
name: kw:brainstorm
description: Brain dump and compile knowledge before structuring a plan. Use when starting any non-trivial knowledge work — after a meeting, when tackling a new problem, or when you need to pull together what you know before planning.
argument-hint: "[topic, brain dump, or meeting notes]"
---

<brain_dump> #$ARGUMENTS </brain_dump>

# Brainstorm

Get everything out of your head and into one place. Pull in references. Find the shape of the problem before you commit to a plan.

## When to Use

* After a meeting where next steps need to be figured out

* Starting a new project, campaign, or strategy

* "I need to think through X", "Let me brain dump", "Help me figure this out"

* When you have scattered inputs (notes, docs, transcripts) that need organizing

## Process

### Step 1: Capture the brain dump

Accept whatever the user gives you. This might be:

* A pasted meeting transcript

* A voice-to-text dump

* Bullet points and half-formed thoughts

* A link to a document

* "Here's what I'm thinking about..."

**Do not organize yet.** Just acknowledge what you received and identify what type of input it is.

If the user hasn't given you anything yet, prompt:

> "What are you working on? You can paste meeting notes, describe the problem, or just start talking. I'll help organize it."

### Step 2: Extract the core elements

From the brain dump, pull out:

* **Key decisions** that need to be made

* **Open questions** that don't have answers yet

* **Constraints** (timeline, budget, dependencies, blockers)

* **Stakeholders** and what they care about

* **Data points** mentioned (numbers, metrics, references)

* **Ideas and options** that were floated (even half-baked ones)

Present these back as a structured summary:

```
## What I Heard

**The problem:** [One sentence — what are we trying to figure out?]

**Decisions to make:**
- [Decision 1]
- [Decision 2]

**Open questions:**
- [Question 1]
- [Question 2]

**Constraints:**
- [Timeline, budget, dependencies]

**Stakeholders:**
- [Who] — [what they care about]

**Ideas floated:**
- [Idea 1] — [brief note on pros/cons if mentioned]
- [Idea 2]

**Data points mentioned:**
- [Any numbers, metrics, or references cited]
```

### Step 3: Pull in references (automatic + optional)

<parallel_tasks>

**Automatic searches** — Run these without asking:

- Search `docs/knowledge/` for learnings related to the brain dump topics
- Search `plans/` for related past plans
- Search `docs/solutions/` for relevant patterns

</parallel_tasks>

For each source found:

```
**Found:** [source name/path]
**Relevant because:** [one sentence]
**Key takeaway:** [the useful bit]
```

If nothing relevant is found: "No prior context found in knowledge base or plans."

**Optional search** — After presenting automatic findings, offer:

> "Want me to search externally too? (web, specific documents, other sources)"

If nothing relevant is found, say so. Don't fabricate context.

### Step 4: Identify themes and tensions

Look across everything — the brain dump, the extracted elements, and the references — and identify:

* **Themes** — What keeps coming up? What's the real underlying question?

* **Tensions** — Where do ideas conflict? Where are there tradeoffs?

* **Gaps** — What's missing? What hasn't been addressed?

```
## Themes
1. [Theme] — [why it matters]
2. [Theme] — [why it matters]

## Tensions
- [Option A] vs [Option B] — [the tradeoff]

## Gaps
- [What we don't know yet]
- [What needs more research]
```

### Step 5: Resolve load-bearing questions

Before moving toward a direction, take the open questions and tensions from Step 2 and Step 4 and identify which ones are **load-bearing** — meaning the plan's structure would change depending on the answer.

Ignore nice-to-know questions. Focus only on ones where different answers lead to different plans. Common load-bearing questions:

- **Scope:** "Is this a quick win or a multi-phase initiative?"
- **Audience:** "Who is this for? That changes everything downstream."
- **Priority:** "You mentioned X and Y — which matters more if we have to choose?"
- **Timeline:** "Are we talking days, weeks, or months?"
- **Owner:** "Who's making the final call on this?"
- **Constraints:** "Is there a budget/resource ceiling I should plan around?"

Use AskUserQuestion to ask **1-3 load-bearing questions at once** (never more than 3). Frame each question with options drawn from what surfaced in the brainstorm — don't ask open-ended questions when you already have candidate answers.

Example:

> **Question:** "You mentioned both 'grow trials' and 'improve conversion' — which is the primary goal?"
> **Options:** Grow trials (top of funnel) / Improve conversion (bottom of funnel) / Both equally

If all open questions are non-load-bearing (i.e., any answer leads to roughly the same plan), skip this step and say so:

> "The open questions won't change the plan's shape — we can resolve them during execution."

**Important:** This step is a bridge, not an interrogation. 1-3 questions max. The goal is to give `/kw:plan` clean inputs, not to turn brainstorming into a requirements gathering session.

### Step 6: Suggest a direction

Based on everything — including the resolved questions from Step 5 — offer a point of view:

> "Based on what I'm seeing, the core question is [X]. The main tension is between [A] and [B]. My suggestion would be to [direction] because [reasoning]. But [caveat]."

This is a suggestion, not a decision. The user decides.

### Step 7: Offer next steps

Use AskUserQuestion:

**Question:** "Brainstorm captured. What next?"

**Options:**

1. **Run `/kw:plan`** — Structure this into an actionable plan
2. **Dig deeper** — Research a specific theme or question further
3. **Push to Proof** — Share the brainstorm for team feedback
4. **Save and continue later** — Write to `plans/brainstorm-{descriptive-name}.md`
5. **Keep going** — Add more context or refine the themes

<critical_requirement>
If "Save" or "Run /kw:plan" is selected: ALWAYS write the brainstorm to `plans/brainstorm-{descriptive-name}.md` first. This file becomes the origin document that `/kw:plan` will search for. Never skip the file write.
</critical_requirement>

## Important Rules

* **Don't jump to solutions.** The point of brainstorming is to understand the problem space before committing to a path. Resist the urge to plan.

* **Reflect, don't rewrite.** When summarizing back, use the user's language. Don't sanitize their thinking into corporate speak.

* **Surface tensions early, resolve the load-bearing ones late.** Steps 2-4 are for naming conflicts without picking winners. Step 5 is for resolving only the ones that would change the plan's shape. Don't collapse tensions prematurely.

* **Pull, don't push.** Ask where references might live rather than guessing. The user knows their information landscape better than you do.

* **Quantity of input is fine.** A 30-minute meeting transcript is good input. Don't ask people to pre-organize before brainstorming — that defeats the purpose.

## Pipeline Mode

When invoked with `disable-model-invocation` context (e.g., from an orchestrator or automation):

- Skip all AskUserQuestion prompts
- Use sensible defaults for all choices
- Write output files without waiting for confirmation
- Proceed to the next suggested skill automatically
- Output structured results that the calling context can parse
