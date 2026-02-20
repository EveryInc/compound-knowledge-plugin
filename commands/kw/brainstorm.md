---
name: kw:brainstorm
description: Brain dump and compile knowledge before structuring a plan. Use when starting any non-trivial knowledge work — after a meeting, when tackling a new problem, or when you need to pull together what you know before planning.
---

# <span data-proof="authored" data-by="ai:claude">Brainstorm</span>

<span data-proof="authored" data-by="ai:claude">Get everything out of your head and into one place. Pull in references. Find the shape of the problem before you commit to a plan.</span>

## <span data-proof="authored" data-by="ai:claude">When to Use</span>

* <span data-proof="authored" data-by="ai:claude">After a meeting where next steps need to be figured out</span>

* <span data-proof="authored" data-by="ai:claude">Starting a new project, campaign, or strategy</span>

* <span data-proof="authored" data-by="ai:claude">"I need to think through X", "Let me brain dump", "Help me figure this out"</span>

* <span data-proof="authored" data-by="ai:claude">When you have scattered inputs (notes, docs, transcripts) that need organizing</span>

## <span data-proof="authored" data-by="ai:claude">Process</span>

### <span data-proof="authored" data-by="ai:claude">Step 1: Capture the brain dump</span>

<span data-proof="authored" data-by="ai:claude">Accept whatever the user gives you. This might be:</span>

* <span data-proof="authored" data-by="ai:claude">A pasted meeting transcript</span>

* <span data-proof="authored" data-by="ai:claude">A voice-to-text dump</span>

* <span data-proof="authored" data-by="ai:claude">Bullet points and half-formed thoughts</span>

* <span data-proof="authored" data-by="ai:claude">A link to a document</span>

* <span data-proof="authored" data-by="ai:claude">"Here's what I'm thinking about..."</span>

**<span data-proof="authored" data-by="ai:claude">Do not organize yet.</span>** <span data-proof="authored" data-by="ai:claude">Just acknowledge what you received and identify what type of input it is.</span>

<span data-proof="authored" data-by="ai:claude">If the user hasn't given you anything yet, prompt:</span>

> <span data-proof="authored" data-by="ai:claude">"What are you working on? You can paste meeting notes, describe the problem, or just start talking. I'll help organize it."</span>

### <span data-proof="authored" data-by="ai:claude">Step 2: Extract the core elements</span>

<span data-proof="authored" data-by="ai:claude">From the brain dump, pull out:</span>

* **<span data-proof="authored" data-by="ai:claude">Key decisions</span>** <span data-proof="authored" data-by="ai:claude">that need to be made</span>

* **<span data-proof="authored" data-by="ai:claude">Open questions</span>** <span data-proof="authored" data-by="ai:claude">that don't have answers yet</span>

* **<span data-proof="authored" data-by="ai:claude">Constraints</span>** <span data-proof="authored" data-by="ai:claude">(timeline, budget, dependencies, blockers)</span>

* **<span data-proof="authored" data-by="ai:claude">Stakeholders</span>** <span data-proof="authored" data-by="ai:claude">and what they care about</span>

* **<span data-proof="authored" data-by="ai:claude">Data points</span>** <span data-proof="authored" data-by="ai:claude">mentioned (numbers, metrics, references)</span>

* **<span data-proof="authored" data-by="ai:claude">Ideas and options</span>** <span data-proof="authored" data-by="ai:claude">that were floated (even half-baked ones)</span>

<span data-proof="authored" data-by="ai:claude">Present these back as a structured summary:</span>

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

### <span data-proof="authored" data-by="ai:claude">Step 3: Pull in references</span>

<span data-proof="authored" data-by="ai:claude">Ask the user:</span>

> <span data-proof="authored" data-by="ai:claude">"Where might relevant context live? I can search for it."</span>

<span data-proof="authored" data-by="ai:claude">Offer to search:</span>

* **<span data-proof="authored" data-by="ai:claude">Local files</span>** <span data-proof="authored" data-by="ai:claude">—</span> <span data-proof="authored" data-by="ai:claude">`plans/`,</span> <span data-proof="authored" data-by="ai:claude">`docs/`, project directories</span>

* **<span data-proof="authored" data-by="ai:claude">Previous work</span>** <span data-proof="authored" data-by="ai:claude">— grep for related topics in the codebase</span>

* **<span data-proof="authored" data-by="ai:claude">Knowledge base</span>** <span data-proof="authored" data-by="ai:claude">—</span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`</span> <span data-proof="authored" data-by="ai:claude">if it exists (from</span> <span data-proof="authored" data-by="ai:claude">`/kw:compound`)</span>

* **<span data-proof="authored" data-by="ai:claude">Web</span>** <span data-proof="authored" data-by="ai:claude">— search for frameworks, best practices, competitive examples</span>

* **<span data-proof="authored" data-by="ai:claude">Documents</span>** <span data-proof="authored" data-by="ai:claude">— if the user points you to Notion pages, Google Docs, or other sources, fetch and summarize them</span>

<span data-proof="authored" data-by="ai:claude">Run all searches in parallel. For each source found:</span>

```
**Found:** [source name/path]
**Relevant because:** [one sentence]
**Key takeaway:** [the useful bit]
```

<span data-proof="authored" data-by="ai:claude">If nothing relevant is found, say so. Don't fabricate context.</span>

### <span data-proof="authored" data-by="ai:claude">Step 4: Identify themes and tensions</span>

<span data-proof="authored" data-by="ai:claude">Look across everything — the brain dump, the extracted elements, and the references — and identify:</span>

* **<span data-proof="authored" data-by="ai:claude">Themes</span>** <span data-proof="authored" data-by="ai:claude">— What keeps coming up? What's the real underlying question?</span>

* **<span data-proof="authored" data-by="ai:claude">Tensions</span>** <span data-proof="authored" data-by="ai:claude">— Where do ideas conflict? Where are there tradeoffs?</span>

* **<span data-proof="authored" data-by="ai:claude">Gaps</span>** <span data-proof="authored" data-by="ai:claude">— What's missing? What hasn't been addressed?</span>

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

> <span data-proof="authored" data-by="ai:claude">"Based on what I'm seeing, the core question is [X]. The main tension is between [A] and [B]. My suggestion would be to [direction] because [reasoning]. But [caveat]."</span>

<span data-proof="authored" data-by="ai:claude">This is a suggestion, not a decision. The user decides.</span>

### Step 7: Offer next steps

<span data-proof="authored" data-by="ai:claude">Use AskUserQuestion:</span>

**<span data-proof="authored" data-by="ai:claude">Question:</span>** <span data-proof="authored" data-by="ai:claude">"Brainstorm captured. What next?"</span>

**<span data-proof="authored" data-by="ai:claude">Options:</span>**

1. **<span data-proof="authored" data-by="ai:claude">Run</span>** **<span data-proof="authored" data-by="ai:claude">`/kw:plan`</span>** <span data-proof="authored" data-by="ai:claude">— Structure this into an actionable plan</span>
2. **<span data-proof="authored" data-by="ai:claude">Dig deeper</span>** <span data-proof="authored" data-by="ai:claude">— Research a specific theme or question further</span>
3. **<span data-proof="authored" data-by="ai:claude">Save as-is</span>** <span data-proof="authored" data-by="ai:claude">— Write the brainstorm to a file for later</span>
4. **<span data-proof="authored" data-by="ai:claude">Keep going</span>** <span data-proof="authored" data-by="ai:claude">— Add more context or refine the themes</span>

<span data-proof="authored" data-by="ai:claude">If "Save as-is": write to</span> <span data-proof="authored" data-by="ai:claude">`plans/brainstorm-{descriptive-name}.md`</span>

<span data-proof="authored" data-by="ai:claude">If "Run</span> <span data-proof="authored" data-by="ai:claude">`/kw:plan`": pass the structured brainstorm as input context.</span>

## <span data-proof="authored" data-by="ai:claude">Important Rules</span>

* **<span data-proof="authored" data-by="ai:claude">Don't jump to solutions.</span>** <span data-proof="authored" data-by="ai:claude">The point of brainstorming is to understand the problem space before committing to a path. Resist the urge to plan.</span>

* **<span data-proof="authored" data-by="ai:claude">Reflect, don't rewrite.</span>** <span data-proof="authored" data-by="ai:claude">When summarizing back, use the user's language. Don't sanitize their thinking into corporate speak.</span>

* **Surface tensions early, resolve the load-bearing ones late.** Steps 2-4 are for naming conflicts without picking winners. Step 5 is for resolving only the ones that would change the plan's shape. Don't collapse tensions prematurely.

* **<span data-proof="authored" data-by="ai:claude">Pull, don't push.</span>** <span data-proof="authored" data-by="ai:claude">Ask where references might live rather than guessing. The user knows their information landscape better than you do.</span>

* **<span data-proof="authored" data-by="ai:claude">Quantity of input is fine.</span>** <span data-proof="authored" data-by="ai:claude">A 30-minute meeting transcript is good input. Don't ask people to pre-organize before brainstorming — that defeats the purpose.</span>