---
name: kw:plan
description: Research past work and structure a knowledge work plan. Use when starting strategy docs, campaign plans, content briefs, research synthesis, or operational playbooks.
---

# <span data-proof="authored" data-by="ai:claude">Plan</span>

<span data-proof="authored" data-by="ai:claude">Research what you already know, then structure a plan grounded in data and past learnings. Lead with the answer.</span>

## <span data-proof="authored" data-by="ai:claude">When to Use</span>

* <span data-proof="authored" data-by="ai:claude">After brainstorming, when you're ready to commit to a direction</span>

* <span data-proof="authored" data-by="ai:claude">Starting a new strategy doc, campaign plan, or brief</span>

* <span data-proof="authored" data-by="ai:claude">"Plan the March campaign", "I need a brief for X", "Let's structure this"</span>

* <span data-proof="authored" data-by="ai:claude">Any non-trivial knowledge work that benefits from past context</span>

## <span data-proof="authored" data-by="ai:claude">Process</span>

### <span data-proof="authored" data-by="ai:claude">Step 1: Classify the work type (auto-detect, don't ask)</span>

<span data-proof="authored" data-by="ai:claude">Determine the work type from the user's description:</span>

| <span data-proof="authored" data-by="ai:claude">Type</span>           | <span data-proof="authored" data-by="ai:claude">Signals</span>                                          |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **<span data-proof="authored" data-by="ai:claude">Strategy</span>**   | <span data-proof="authored" data-by="ai:claude">Roadmap, architecture, long-term, layers, phases</span> |
| **<span data-proof="authored" data-by="ai:claude">Campaign</span>**   | <span data-proof="authored" data-by="ai:claude">Launch, promotion, timeline, channels, audience</span>  |
| **<span data-proof="authored" data-by="ai:claude">Brief</span>**      | <span data-proof="authored" data-by="ai:claude">Directive for someone else, scope, deliverables</span>  |
| **<span data-proof="authored" data-by="ai:claude">Research</span>**   | <span data-proof="authored" data-by="ai:claude">Investigation, competitive, analysis, synthesis</span>  |
| **<span data-proof="authored" data-by="ai:claude">Operations</span>** | <span data-proof="authored" data-by="ai:claude">Playbook, runbook, SOP, recurring process</span>        |

<span data-proof="authored" data-by="ai:claude">Pick the best fit and proceed. Do not ask the user to classify.</span>

### <span data-proof="authored" data-by="ai:claude">Step 2: Research (all in parallel)</span>

<span data-proof="authored" data-by="ai:claude">Run ALL of these searches simultaneously:</span>

**<span data-proof="authored" data-by="ai:claude">2a. Past plans</span>** <span data-proof="authored" data-by="ai:claude">— Search</span> <span data-proof="authored" data-by="ai:claude">`plans/`</span> <span data-proof="authored" data-by="ai:claude">for related work:</span>

```
Glob: plans/*.md
Grep: [keywords from description] in plans/
```

<span data-proof="authored" data-by="ai:claude">Read the top 3 most relevant files. Extract: what was decided, what data was used, what worked.</span>

**<span data-proof="authored" data-by="ai:claude">2b. Knowledge base</span>** <span data-proof="authored" data-by="ai:claude">— Search</span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`</span> <span data-proof="authored" data-by="ai:claude">for saved learnings:</span>

```
Grep: [keywords] in docs/knowledge/
```

<span data-proof="authored" data-by="ai:claude">These are insights from past sessions saved by</span> <span data-proof="authored" data-by="ai:claude">`/kw:compound`. They exist because someone thought they were worth remembering.</span>

**<span data-proof="authored" data-by="ai:claude">2c. Solutions and patterns</span>** <span data-proof="authored" data-by="ai:claude">— Search</span> <span data-proof="authored" data-by="ai:claude">`docs/solutions/`</span> <span data-proof="authored" data-by="ai:claude">for relevant patterns:</span>

```
Grep: [keywords] in docs/solutions/
```

<span data-proof="authored" data-by="ai:claude">Engineering patterns, but may contain relevant operational or integration insights.</span>

**<span data-proof="authored" data-by="ai:claude">2d. Live data</span>** <span data-proof="authored" data-by="ai:claude">— Pull current metrics if the plan involves data.</span>

<span data-proof="authored" data-by="ai:claude">Follow whatever data hierarchy exists in the project's CLAUDE.md. If none exists, ask the user where to find relevant data.</span>

**<span data-proof="authored" data-by="ai:claude">2e. External research</span>** <span data-proof="authored" data-by="ai:claude">— If the topic would benefit from outside context (competitive analysis, best practices, frameworks), search the web.</span>

### <span data-proof="authored" data-by="ai:claude">Step 3: Surface what you already know</span>

<span data-proof="authored" data-by="ai:claude">Before writing anything, present a context brief:</span>

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

<span data-proof="authored" data-by="ai:claude">Wait for the user to react. They may refine direction, add context, or say "looks good, go."</span>

### <span data-proof="authored" data-by="ai:claude">Step 4: Structure the plan</span>

<span data-proof="authored" data-by="ai:claude">Use this template. Lead with the recommendation (Pyramid Principle — answer first, then supporting logic). Fill sections based on research findings. Skip sections that aren't relevant.</span>

```markdown proof:W3sidHlwZSI6InByb29mQXV0aG9yZWQiLCJmcm9tIjowLCJ0byI6ODYyLCJhdHRycyI6eyJieSI6ImFpOmNsYXVkZSJ9fV0=
# [Plan Title]

**Type:** [Strategy | Campaign | Brief | Research | Operations]
**Status:** Draft
**Created:** [today's date]

---

## Recommendation

[One paragraph: what we should do and why. Lead with the answer.]

## Current State

[What's true right now. Data from Step 2d.]
[Include source and date for every number.]

## Proposed Approach

[How to get from current state to the desired outcome.]
[For strategies: layers or phases.]
[For campaigns: channels, timeline, assets.]
[For briefs: scope, deliverables, constraints.]

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

### <span data-proof="authored" data-by="ai:claude">Step 5: Write to plans/</span>

* <span data-proof="authored" data-by="ai:claude">Filename:</span> <span data-proof="authored" data-by="ai:claude">`plans/{type}-{descriptive-name}.md`</span>

* <span data-proof="authored" data-by="ai:claude">If filename already exists, append date:</span> <span data-proof="authored" data-by="ai:claude">`plans/{type}-{name}-{YYYY-MM-DD}.md`</span>

* <span data-proof="authored" data-by="ai:claude">Always write the file BEFORE presenting options.</span>

### <span data-proof="authored" data-by="ai:claude">Step 6: Offer next steps</span>

<span data-proof="authored" data-by="ai:claude">Use AskUserQuestion:</span>

**<span data-proof="authored" data-by="ai:claude">Question:</span>** <span data-proof="authored" data-by="ai:claude">"Plan written to</span> <span data-proof="authored" data-by="ai:claude">`plans/{filename}`. What next?"</span>

**<span data-proof="authored" data-by="ai:claude">Options:</span>**

1. **<span data-proof="authored" data-by="ai:claude">Run</span>** **<span data-proof="authored" data-by="ai:claude">`/kw:review`</span>** <span data-proof="authored" data-by="ai:claude">— Check strategic alignment and data accuracy</span>
2. **<span data-proof="authored" data-by="ai:claude">Start</span>** **<span data-proof="authored" data-by="ai:claude">`/kw:work`</span>** <span data-proof="authored" data-by="ai:claude">— Begin executing this plan</span>
3. **<span data-proof="authored" data-by="ai:claude">Refine</span>** <span data-proof="authored" data-by="ai:claude">— Adjust specific sections</span>
4. **<span data-proof="authored" data-by="ai:claude">Open in editor</span>** <span data-proof="authored" data-by="ai:claude">— View the full plan</span>

## <span data-proof="authored" data-by="ai:claude">Important Rules</span>

* **<span data-proof="authored" data-by="ai:claude">Lead with the answer.</span>** <span data-proof="authored" data-by="ai:claude">The Recommendation section comes first, not last. If someone only reads one paragraph, they should know what you're proposing.</span>

* **<span data-proof="authored" data-by="ai:claude">Cite everything.</span>** <span data-proof="authored" data-by="ai:claude">Every data point needs a source. "+32% WoW" not "+32%".</span>

* **<span data-proof="authored" data-by="ai:claude">Surface past work.</span>** <span data-proof="authored" data-by="ai:claude">The whole point is that knowledge compounds. If related plans or learnings exist, they MUST appear in the context brief.</span>

* **<span data-proof="authored" data-by="ai:claude">Don't over-template.</span>** <span data-proof="authored" data-by="ai:claude">The template is a starting point. Skip sections that don't apply. A campaign plan doesn't need an "Architecture" section.</span>

* **<span data-proof="authored" data-by="ai:claude">Degrade gracefully.</span>** <span data-proof="authored" data-by="ai:claude">If a data source fails or returns nothing, proceed with what you have. Note what's missing.</span>