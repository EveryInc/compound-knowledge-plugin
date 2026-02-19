# <span data-proof="authored" data-by="ai:claude">Compound Knowledge</span>

<span data-proof="authored" data-by="ai:claude">AI-powered workflows for knowledge work: brainstorm, plan, review, execute, and save learnings. The knowledge work equivalent of</span> [<span data-proof="authored" data-by="ai:claude">Compound Engineering</span>](https://github.com/EveryInc/compound-engineering-plugin)<span data-proof="authored" data-by="ai:claude">.</span>

## <span data-proof="authored" data-by="ai:claude">The Loop</span>

```
/workflows:brainstorm  →  Brain dump, pull references, find the shape
/workflows:plan        →  Structure into an actionable plan
/workflows:review      →  Strategic alignment + data accuracy check
/workflows:work        →  Execute the plan, produce deliverables
/workflows:compound    →  Save learnings for next time
```

<span data-proof="authored" data-by="ai:claude">Each cycle makes the next one faster.</span> <span data-proof="authored" data-by="ai:claude">`/workflows:plan`</span> <span data-proof="authored" data-by="ai:claude">searches</span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`</span> <span data-proof="authored" data-by="ai:claude">for past learnings saved by</span> <span data-proof="authored" data-by="ai:claude">`/workflows:compound`. Knowledge compounds.</span>

## <span data-proof="authored" data-by="ai:claude">Install</span>

<span data-proof="authored" data-by="ai:claude">Add to your Claude Code plugins:</span>

```bash proof:W3sidHlwZSI6InByb29mQXV0aG9yZWQiLCJmcm9tIjowLCJ0byI6NTMsImF0dHJzIjp7ImJ5IjoiYWk6Y2xhdWRlIn19XQ==
claude plugins add EveryInc/compound-knowledge-plugin
```

## <span data-proof="authored" data-by="ai:claude">Workflows</span>

### <span data-proof="authored" data-by="ai:claude">Brainstorm</span>

<span data-proof="authored" data-by="ai:claude">Start here. Paste a meeting transcript, brain dump raw thoughts, or describe a problem. The agent extracts key decisions, open questions, constraints, and tensions — then pulls in references from your project.</span>

```
/workflows:brainstorm
```

### <span data-proof="authored" data-by="ai:claude">Plan</span>

<span data-proof="authored" data-by="ai:claude">Structure a brainstorm into an actionable plan. Searches past plans, knowledge base, and external sources. Outputs a Pyramid Principle plan (lead with the answer).</span>

```
/workflows:plan
```

### <span data-proof="authored" data-by="ai:claude">Review</span>

<span data-proof="authored" data-by="ai:claude">Two reviewers check your work:</span>

* **<span data-proof="authored" data-by="ai:claude">Strategic Alignment</span>** <span data-proof="authored" data-by="ai:claude">— Is the goal clear? Is the hypothesis falsifiable? Are we solving the right problem?</span>

* **<span data-proof="authored" data-by="ai:claude">Data Accuracy</span>** <span data-proof="authored" data-by="ai:claude">— Are numbers sourced? Are baselines explicit? Is data fresh?</span>

<span data-proof="authored" data-by="ai:claude">Findings are grouped P1 (blocks shipping) / P2 (should fix) / P3 (nice to have).</span>

```
/workflows:review
```

### <span data-proof="authored" data-by="ai:claude">Work</span>

<span data-proof="authored" data-by="ai:claude">Execute a plan. Break it into tasks, produce deliverables one at a time, track what happened.</span>

```
/workflows:work
```

### <span data-proof="authored" data-by="ai:claude">Compound</span>

<span data-proof="authored" data-by="ai:claude">Extract 1-3 learnings from a session and save them to</span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`. These get surfaced automatically next time</span> <span data-proof="authored" data-by="ai:claude">`/workflows:plan`</span> <span data-proof="authored" data-by="ai:claude">runs on a related topic.</span>

```
/workflows:compound
```

## <span data-proof="authored" data-by="ai:claude">How It Works</span>

<span data-proof="authored" data-by="ai:claude">The compounding loop:</span>

1. <span data-proof="authored" data-by="ai:claude">You brainstorm and plan something</span>
2. <span data-proof="authored" data-by="ai:claude">`/workflows:plan`</span> <span data-proof="authored" data-by="ai:claude">searches</span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`</span> <span data-proof="authored" data-by="ai:claude">— finds past insights</span>
3. <span data-proof="authored" data-by="ai:claude">You execute and review</span>
4. <span data-proof="authored" data-by="ai:claude">`/workflows:compound`</span> <span data-proof="authored" data-by="ai:claude">saves what you learned to</span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`</span>
5. <span data-proof="authored" data-by="ai:claude">Next time you plan something related, step 2 finds it</span>

<span data-proof="authored" data-by="ai:claude">No configuration needed. Works with any project that has a</span> <span data-proof="authored" data-by="ai:claude">`plans/`</span> <span data-proof="authored" data-by="ai:claude">directory.</span>

## <span data-proof="authored" data-by="ai:claude">Customization</span>

<span data-proof="authored" data-by="ai:claude">The plugin reads your project's</span> <span data-proof="authored" data-by="ai:claude">`CLAUDE.md`</span> <span data-proof="authored" data-by="ai:claude">for:</span>

* <span data-proof="authored" data-by="ai:claude">Business context and goals (used by the strategic alignment reviewer)</span>

* <span data-proof="authored" data-by="ai:claude">Data source hierarchy (used by the data accuracy reviewer)</span>

* <span data-proof="authored" data-by="ai:claude">Style guides and conventions (used during execution)</span>

<span data-proof="authored" data-by="ai:claude">If your project doesn't have a</span> <span data-proof="authored" data-by="ai:claude">`CLAUDE.md`, the workflows still work — they just won't have project-specific context.</span>

## <span data-proof="authored" data-by="ai:claude">Components</span>

| <span data-proof="authored" data-by="ai:claude">Type</span>          | <span data-proof="authored" data-by="ai:claude">Count</span> | <span data-proof="authored" data-by="ai:claude">Description</span>                              |
| -------------------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| <span data-proof="authored" data-by="ai:claude">Workflows</span>     | <span data-proof="authored" data-by="ai:claude">5</span>     | <span data-proof="authored" data-by="ai:claude">brainstorm, plan, review, work, compound</span> |
| <span data-proof="authored" data-by="ai:claude">Review Agents</span> | <span data-proof="authored" data-by="ai:claude">2</span>     | <span data-proof="authored" data-by="ai:claude">strategic-alignment, data-accuracy</span>       |

## <span data-proof="authored" data-by="ai:claude">License</span>

<span data-proof="authored" data-by="ai:claude">MIT</span>