# Compound Knowledge

Knowledge compounds. Each cycle of planning makes the next one faster — because what you learn gets saved and surfaced automatically.

This is a [Claude Code](https://claude.ai/claude-code) plugin that adds AI-powered workflows for knowledge work: strategy docs, campaign plans, content briefs, research synthesis, and operational playbooks.

Built by [Austin Tedesco](https://every.to) at [Every](https://every.to). Read the story: [How to Build a Command Center That Keeps You Sane](https://every.to/p/how-to-build-a-command-center-that-keeps-you-sane).

## Install

Inside a Claude Code session:

```
/plugin marketplace add EveryInc/compound-knowledge-plugin
/plugin install compound-knowledge
```

## The Loop

```
brainstorm  -->  plan  -->  review  -->  work  -->  compound
    ^                                                  |
    '--------------- next cycle finds it --------------'
```

`/kw:compound` saves what you learned. `/kw:plan` finds it next time. The loop gets smarter.

## What's Inside

6 skills and 5 agents. See the [full documentation](plugins/compound-knowledge/README.md) for details.

| Skill | What it does |
|-------|-------------|
| `/kw:brainstorm` | Brain dump, pull references, find the shape |
| `/kw:plan` | Research past work, structure an actionable plan |
| `/kw:confidence` | Gut-check what you know vs. don't |
| `/kw:review` | Strategic alignment + data accuracy check |
| `/kw:work` | Execute the plan, produce deliverables |
| `/kw:compound` | Save learnings for next time |

## License

MIT
