# Compound Knowledge

Knowledge compounds. Brainstorm, plan, review, execute, and save what you learn — so the next cycle starts smarter.

The knowledge work equivalent of [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin).

## The Loop

```
brainstorm  -->  plan  -->  review  -->  work  -->  compound
    ^                                                  |
    '--------------- next cycle finds it --------------'
```

Each step feeds the next. `/kw:compound` saves what you learned to `docs/knowledge/`. Next time `/kw:plan` runs, it searches that directory automatically — surfacing past insights, corrections, and patterns without you having to remember they exist.

## How It Works

Context switching kills productivity. By the time you gather everything you need to think, you're fried. You have nothing left for the decisions that matter.

This plugin gives you a system where knowledge accumulates instead of evaporating. The first plan takes effort. The tenth plan on a related topic starts with everything you've already learned — surfaced automatically, not from memory.

The secret is `docs/knowledge/`. It's a directory of plain markdown files with YAML frontmatter, each capturing one insight from a past session. When you plan something new, the plugin greps this directory and brings relevant learnings into the conversation before you write a word.

No configuration needed. No database. No API keys. Just markdown files in your project, version-controlled by git.

## Components

| Type | Count | Description |
|------|-------|-------------|
| Skills | 6 | brainstorm, plan, confidence, review, work, compound |
| Review Agents | 2 | strategic-alignment, data-accuracy |
| Research Agents | 3 | past-work-researcher, knowledge-base-researcher, stale-knowledge-checker |

## Skills

| Skill | Description | When to use |
|-------|-------------|-------------|
| `/kw:brainstorm` | Brain dump and compile knowledge before planning. Auto-searches your knowledge base and past plans for relevant context. | After a meeting, starting a new project, or when you need to organize scattered inputs |
| `/kw:plan` | Research past work and structure an actionable plan. Launches parallel research agents, then structures using Pyramid Principle templates (Strategy, Campaign, Brief, Research, Operations). | When you're ready to commit to a direction and need a structured plan |
| `/kw:confidence` | Pause and honestly assess what you know and don't know. Non-destructive interrupt — callable at any point in the loop. | Before committing to a plan, when something feels uncertain, as a gut-check during any workflow |
| `/kw:review` | Two reviewers check your work in parallel: Strategic Alignment (right problem? right approach?) and Data Accuracy (numbers sourced? data fresh?). | Before sharing a plan or strategy doc with stakeholders |
| `/kw:work` | Execute a plan. Break into tasks, group by dependency, run independent tasks in parallel. Writes execution log to the plan file. | After planning and review — time to produce deliverables |
| `/kw:compound` | Extract 1-3 learnings from a session. Checks for stale knowledge that the new learning contradicts. Saves to `docs/knowledge/` with searchable YAML frontmatter. | At the end of any meaningful work session |

## Agents

### Review

| Agent | Description |
|-------|-------------|
| `strategic-alignment-reviewer` | Evaluates plans against organizational goals. Checks goal clarity, hypothesis falsifiability, success metrics, scope proportionality, resource awareness, opportunity cost. |
| `data-accuracy-reviewer` | Verifies every number, source, and data claim. Checks source citations, comparison baselines, canonical definitions, freshness, caveats, hardcoded values. |

### Research

| Agent | Description |
|-------|-------------|
| `past-work-researcher` | Searches `plans/` and `docs/solutions/` for related prior work. Finds what was decided, what data was used, and what worked. |
| `knowledge-base-researcher` | Searches `docs/knowledge/` for saved learnings. This is the agent that closes the compounding loop. |
| `stale-knowledge-checker` | After a new learning is extracted, checks `docs/knowledge/` for entries that the new learning contradicts or supersedes. Prevents knowledge base from accumulating contradictions. |

## Getting Started

### 1. Install the plugin

```
/plugin marketplace add EveryInc/compound-knowledge-plugin
/plugin install compound-knowledge
```

### 2. Try a brainstorm

Start with whatever is on your mind. A problem you're solving, a campaign you're planning, notes from a meeting:

```
/kw:brainstorm I need to figure out our Q2 content strategy. We're seeing declining engagement on long-form but short-form clips are performing well. Not sure whether to double down on video or fix the written content.
```

The plugin will extract key decisions, tensions, and open questions — then automatically search your project for relevant past work and knowledge.

### 3. Structure a plan

When you're ready to commit to a direction:

```
/kw:plan
```

This launches parallel research agents, finds past learnings, and structures everything into a Pyramid Principle plan (lead with the answer). Three detail tiers — Quick for gut checks, Standard for most plans, Deep for multi-quarter strategies.

### 4. Save what you learned

After any meaningful session:

```
/kw:compound
```

This extracts insights, checks for conflicts with existing knowledge, and saves to `docs/knowledge/`. Next time you plan something related, these learnings surface automatically.

## The Compounding Loop

The core mechanism:

1. `/kw:compound` saves learnings to `docs/knowledge/{slug}.md` with YAML frontmatter
2. `/kw:brainstorm` auto-searches `docs/knowledge/` when you start a new brainstorm
3. `/kw:plan` launches `knowledge-base-researcher` to find relevant learnings
4. Stale knowledge checker prevents contradictions from accumulating
5. Each cycle is faster because context is already there

The knowledge files are plain markdown, git-tracked, and greppable. No external dependencies.

```yaml
# Example: docs/knowledge/trial-conversion-timing.md
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

## Context
Discovered during the January 30-day trial campaign analysis.

## Implication
When planning trial campaigns, factor in the 60-day lag before comparing
against shorter trial periods.
```

## Customization

The plugin reads your project's `CLAUDE.md` for:

- **Business context and goals** — used by the strategic alignment reviewer
- **Data source hierarchy** — used by the data accuracy reviewer
- **Style guides and conventions** — used during execution

If your project doesn't have a `CLAUDE.md`, the workflows still work — they just won't have project-specific context.

## Installation

Requires [Claude Code](https://claude.ai/claude-code).

```
/plugin marketplace add EveryInc/compound-knowledge-plugin
/plugin install compound-knowledge
```

Restart Claude Code after installation to load the plugin.

## License

MIT
