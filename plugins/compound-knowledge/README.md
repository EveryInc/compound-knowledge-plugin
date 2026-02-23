# Compound Knowledge

AI-powered workflows for knowledge work: brainstorm, plan, review, execute, and save learnings. The knowledge work equivalent of [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin).

## The Loop

```
/kw:brainstorm  →  Brain dump, pull references, find the shape
/kw:plan        →  Structure into an actionable plan
/kw:review      →  Strategic alignment + data accuracy check
/kw:work        →  Execute the plan, produce deliverables
/kw:compound    →  Save learnings for next time
```

Each cycle makes the next one faster. `/kw:plan` searches `docs/knowledge/` for past learnings saved by `/kw:compound`. Knowledge compounds.

## Install

Inside a [Claude Code](https://claude.ai/claude-code) session, run:

```
/plugin marketplace add EveryInc/compound-knowledge-plugin
/plugin install compound-knowledge@compound-knowledge-marketplace
```

Then restart Claude Code to load the plugin.

## Workflows

### Brainstorm

Start here. Paste a meeting transcript, brain dump raw thoughts, or describe a problem. The agent extracts key decisions, open questions, constraints, and tensions — then pulls in references from your project.

```
/kw:brainstorm
```

### Plan

Structure a brainstorm into an actionable plan. Searches past plans, knowledge base, and external sources. Outputs a Pyramid Principle plan (lead with the answer).

```
/kw:plan
```

### Review

Two reviewers check your work **in parallel**:

* **Strategic Alignment** — Is the goal clear? Is the hypothesis falsifiable? Are we solving the right problem?

* **Data Accuracy** — Are numbers sourced? Are baselines explicit? Is data fresh?

Both run simultaneously as Task agents, then findings are merged and grouped P1 (blocks shipping) / P2 (should fix) / P3 (nice to have).

```
/kw:review
```

### Work

Execute a plan. Break it into tasks, group by dependency, and run independent tasks in parallel. Dependent tasks run sequentially with approval gates between batches.

```
/kw:work
```

### Compound

Extract 1-3 learnings from a session and save them to `docs/knowledge/`. These get surfaced automatically next time `/kw:plan` runs on a related topic.

```
/kw:compound
```

## How It Works

The compounding loop:

1. You brainstorm and plan something
2. `/kw:plan` searches `docs/knowledge/` — finds past insights
3. You execute and review
4. `/kw:compound` saves what you learned to `docs/knowledge/`
5. Next time you plan something related, step 2 finds it

No configuration needed. Works with any project that has a `plans/` directory.

## Customization

The plugin reads your project's `CLAUDE.md` for:

* Business context and goals (used by the strategic alignment reviewer)

* Data source hierarchy (used by the data accuracy reviewer)

* Style guides and conventions (used during execution)

If your project doesn't have a `CLAUDE.md`, the workflows still work — they just won't have project-specific context.

## Components

| Type          | Count | Description                              |
| ------------- | ----- | ---------------------------------------- |
| Workflows     | 5     | brainstorm, plan, review, work, compound |
| Review Agents | 2     | strategic-alignment, data-accuracy       |

## License

MIT