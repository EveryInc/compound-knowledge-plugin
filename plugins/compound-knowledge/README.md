# Compound Knowledge

AI-powered workflows for knowledge work: brainstorm, plan, review, execute, and save learnings. The knowledge work equivalent of [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin).

## The Loop

```
/kw:brainstorm   -->  Brain dump, pull references, find the shape
/kw:plan         -->  Structure into an actionable plan
/kw:confidence   -->  Gut-check what you know vs. don't (callable at any point)
/kw:review       -->  Strategic alignment + data accuracy check
/kw:work         -->  Execute the plan, produce deliverables
/kw:compound     -->  Save learnings for next time
```

Each cycle makes the next one faster. `/kw:plan` searches `docs/knowledge/` for past learnings saved by `/kw:compound`. Knowledge compounds.

## Install

Inside a [Claude Code](https://claude.ai/claude-code) session:

```
/plugin marketplace add EveryInc/compound-knowledge-plugin
/plugin install compound-knowledge
```

## Getting Started

Brainstorm something. A problem, a campaign, notes from a meeting:

```
/kw:brainstorm I need to figure out our Q2 content strategy
```

When you're ready to commit to a direction:

```
/kw:plan
```

After any meaningful session, save what you learned:

```
/kw:compound
```

Next time you brainstorm or plan something related, those learnings surface automatically.

## Workflows

### Brainstorm

Start here. Paste a meeting transcript, brain dump raw thoughts, or describe a problem. Auto-searches your knowledge base and past plans for relevant context, then extracts key decisions, open questions, constraints, and tensions.

### Plan

Structure a brainstorm into an actionable plan. Launches parallel research agents to find past work and saved learnings. Outputs a Pyramid Principle plan (lead with the answer) in three detail tiers — Quick for gut checks, Standard for most plans, Deep for multi-quarter strategies.

### Confidence

Callable at any point in the loop. Pauses to honestly assess what Claude knows and doesn't know — in plain language, not a table. Produces a "confident about / less confident about / my recommendation" breakdown, then offers specific actions to close gaps.

### Review

Two reviewers check your work **in parallel**:

* **Strategic Alignment** — Is the goal clear? Is the hypothesis falsifiable? Are we solving the right problem?
* **Data Accuracy** — Are numbers sourced? Are baselines explicit? Is data fresh?

Findings are merged and grouped P1 (blocks shipping) / P2 (should fix) / P3 (nice to have).

### Work

Execute a plan. Break it into tasks, group by dependency, run independent tasks in parallel. Writes execution log back to the plan file so `/kw:compound` has concrete material to learn from.

### Compound

Extract 1-3 learnings from a session. Checks for stale knowledge that the new learning contradicts. Saves to `docs/knowledge/` with searchable YAML frontmatter.

## How It Works

1. You brainstorm and plan something
2. `/kw:plan` searches `docs/knowledge/` — finds past insights
3. You execute and review
4. `/kw:compound` saves what you learned to `docs/knowledge/`
5. Next time you plan something related, step 2 finds it

No configuration needed. Works with any project that has a `plans/` directory.

The knowledge files are plain markdown, git-tracked, and greppable:

```yaml
# docs/knowledge/trial-conversion-timing.md
---
type: insight
tags: [trials, conversion, campaigns]
confidence: high
created: 2026-02-15
source: Q1 trial campaign analysis
---

# Trial Conversion Timing

Extended trial periods (30 days vs 7 days) increase conversion rate but
delay revenue recognition. Net positive after 60 days.
```

## Components

| Type | Count | Description |
|------|-------|-------------|
| Skills | 6 | brainstorm, plan, confidence, review, work, compound |
| Review Agents | 2 | strategic-alignment, data-accuracy |
| Research Agents | 3 | past-work-researcher, knowledge-base-researcher, stale-knowledge-checker |

## Customization

The plugin reads your project's `CLAUDE.md` for:

* Business context and goals (used by the strategic alignment reviewer)
* Data source hierarchy (used by the data accuracy reviewer)
* Style guides and conventions (used during execution)

If your project doesn't have a `CLAUDE.md`, the workflows still work — they just won't have project-specific context.

## License

MIT
