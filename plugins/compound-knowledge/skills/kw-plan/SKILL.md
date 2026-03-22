---
name: kw:plan
description: Research past work and structure a knowledge work plan. Use when starting strategy docs, campaign plans, content briefs, research synthesis, or operational playbooks.
argument-hint: "[what to plan]"
---

<plan_request> #$ARGUMENTS </plan_request>

# Plan

Research what you already know, then structure a plan grounded in data and past learnings. Lead with the answer.

## When to Use

* After brainstorming, when you're ready to commit to a direction

* Starting a new strategy doc, campaign plan, or brief

* "Plan the March campaign", "I need a brief for X", "Let's structure this"

* Any non-trivial knowledge work that benefits from past context

## Process

### Step 1: Classify the work type (auto-detect, don't ask)

Determine the work type from the user's description:

| Type           | Signals                                          |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Strategy**   | Roadmap, architecture, long-term, layers, phases |
| **Campaign**   | Launch, promotion, timeline, channels, audience  |
| **Brief**      | Directive for someone else, scope, deliverables  |
| **Research**   | Investigation, competitive, analysis, synthesis  |
| **Operations** | Playbook, runbook, SOP, recurring process        |

Pick the best fit and proceed. Do not ask the user to classify.

Also determine the **detail tier** from scope signals:

| Tier | Signals | Output |
|------|---------|--------|
| **Quick** | "should we?", "gut check", single question, <30 min scope | Title, recommendation, 2-3 bullets of reasoning, one success metric |
| **Standard** | Default — most plans | Full template for the work type |
| **Deep** | "restructure", "strategy", "multi-quarter", "fundamental" | Full template + research appendix, competitive analysis, risk matrix, phased timeline |

Pick the best fit. Default to Standard if unclear.

### Step 2: Research (parallel agents + inline)

Launch research agents in parallel. Each returns structured findings — they do NOT write files.

<parallel_tasks>

**2a. Past work** — Launch Task agent: `compound-knowledge:research:past-work-researcher`
- Pass: the plan request description + work type from Step 1
- Returns: related plans, prior decisions, origin brainstorm documents

**2b. Knowledge base** — Launch Task agent: `compound-knowledge:research:knowledge-base-researcher`
- Pass: the plan request description + keywords
- Returns: saved learnings from docs/knowledge/ (insights, corrections, playbooks, patterns)

**2c. External research** (inline, not an agent) — If the topic would benefit from outside context:
- Search the web for frameworks, best practices, competitive examples
- Only run if the topic is outward-facing or novel — skip for internal operations

</parallel_tasks>

**2d. Live data** — Pull current metrics if the plan involves data. Follow whatever data hierarchy exists in the project's CLAUDE.md. If none exists, ask the user where to find relevant data.

**2e. Origin document check** — Search for `plans/brainstorm-*.md` files matching this topic. If found, this brainstorm is the origin document — reference it throughout the plan as `(see origin: plans/brainstorm-{name}.md)` and cross-check that the plan addresses tensions and load-bearing questions from the brainstorm.

Wait for all parallel tasks to complete before proceeding.

### Step 3: Surface what you already know

Before writing anything, present a context brief:

```
## What I Found

**Related plans:**
- [plan name] — [one-line summary of what's relevant]

**Past learnings:**
- [learning title] — [the insight]

**Current data:**
- [metric]: [value] ([source, date])

**External research:**
- [finding] — [source]

**No prior context found** (if searches returned nothing)
```

Wait for the user to react. They may refine direction, add context, or say "looks good, go."

### Step 4: Structure the plan

Use the template that matches the work type from Step 1. Each type has a different lead section — use the right one. Fill sections based on research findings. Skip sections that aren't relevant.

**All templates share these common sections** (include at the bottom of every plan):

```markdown
## Success Metrics

| Metric | Current Baseline | Target | Source |
|--------|-----------------|--------|--------|
| [Primary metric] | [value] | [goal] | [where to measure] |

## Open Questions

- [What we don't know yet]
- [Decisions that need to be made]

## References

- [Related plans, knowledge entries, data sources used]
```

***

**Strategy** — Pyramid Principle. Lead with the recommendation.

```markdown
# [Plan Title]

**Type:** Strategy
**Status:** Draft
**Created:** [today's date]

---

## Recommendation

[One paragraph: what we should do and why. Lead with the answer.]

## Current State

[What's true right now. Data from Step 2d. Source and date for every number.]

## Proposed Approach

[How to get from current state to the desired outcome. Layers or phases.]
```

***

**Campaign** — Timeline-first. Lead with what launches when.

```markdown
# [Plan Title]

**Type:** Campaign
**Status:** Draft
**Created:** [today's date]

---

## Timeline

| Date/Week | Action | Channel | Owner |
|-----------|--------|---------|-------|
| [date] | [what launches] | [where] | [who] |

## Goal

[One paragraph: what this campaign achieves and how we'll know it worked.]

## Audience

[Who this targets. Segment, persona, or behavioral description.]

## Assets Needed

- [Copy, creative, landing pages, emails — what needs to be produced]

## Current State

[Relevant baselines. What are the numbers before we start?]
```

***

**Brief** — Directive-first. Lead with the recommendation, then scope.

```markdown
# [Plan Title]

**Type:** Brief
**Status:** Draft
**Created:** [today's date]

---

## Recommendation

[One paragraph: what we should do and why. Lead with the answer.]

## Scope

[What's in and what's out. Be explicit about boundaries.]

## Deliverables

- [Concrete output 1]
- [Concrete output 2]

## Constraints

[Timeline, budget, dependencies, blockers.]

## Context

[Background the reader needs. Data from Step 2d.]
```

***

**Research** — Findings-first. Lead with what you discovered.

```markdown
# [Plan Title]

**Type:** Research
**Status:** Draft
**Created:** [today's date]

---

## Key Findings

1. **[Finding]** — [One sentence with data. Source and date.]
2. **[Finding]** — [One sentence with data. Source and date.]
3. **[Finding]** — [One sentence with data. Source and date.]

## Implications

[What these findings mean for the business. What should change.]

## Methodology

[How you gathered this data. Sources, timeframes, filters, caveats.]

## Raw Data

[Tables, charts, or links to dashboards that support the findings.]
```

***

**Operations** — Trigger-first. Lead with when this runs and what to do.

```markdown
# [Plan Title]

**Type:** Operations
**Status:** Draft
**Created:** [today's date]

---

## Trigger

[When does this process run? On a schedule, on an event, on request?]

## Steps

1. [Step] — [details, tools, commands]
2. [Step] — [details, tools, commands]
3. [Step] — [details, tools, commands]

## Edge Cases

| Situation | What to do |
|-----------|-----------|
| [When X happens] | [Do Y] |

## Owner

[Who runs this. Who to escalate to.]

## Dependencies

[What this process needs to work — access, tools, data sources.]
```

### Step 5: Write to plans/

* Filename: `plans/{type}-{descriptive-name}.md`

* If filename already exists, append date: `plans/{type}-{name}-{YYYY-MM-DD}.md`

* Always write the file BEFORE presenting options.

### Step 6: Offer next steps

Use AskUserQuestion:

**Question:** "Plan written to `plans/{filename}`. What next?"

**Options:**

1. **Run `/kw:review`** — Check strategic alignment and data accuracy
2. **Start `/kw:work`** — Begin executing this plan
3. **Push to Proof** — Share the plan for collaborative review
4. **Refine** — Adjust specific sections
5. **Open in editor** — View the full plan

## Important Rules

* **Lead with what the reader needs first.** Strategy/Brief: the recommendation. Campaign: the timeline. Research: the findings. Operations: the trigger and steps. If someone only reads the first section, they should get the most important thing.

* **Cite everything.** Every data point needs a source. "+32% WoW" not "+32%".

* **Surface past work.** The whole point is that knowledge compounds. If related plans or learnings exist, they MUST appear in the context brief.

* **Don't over-template.** The template is a starting point. Skip sections that don't apply. A campaign plan doesn't need an "Architecture" section.

* **Degrade gracefully.** If a data source fails or returns nothing, proceed with what you have. Note what's missing.

## Pipeline Mode

When invoked with `disable-model-invocation` context (e.g., from an orchestrator or automation):

- Skip all AskUserQuestion prompts
- Use sensible defaults for all choices
- Write output files without waiting for confirmation
- Proceed to the next suggested skill automatically
- Output structured results that the calling context can parse
