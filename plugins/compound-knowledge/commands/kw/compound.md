---
name: kw:compound
description: Extract and save learnings from a completed knowledge work session. Saves to docs/knowledge/ so future plans automatically find them.
---

# <span data-proof="authored" data-by="ai:claude">Compound</span>

<span data-proof="authored" data-by="ai:claude">Close the loop. Extract what you learned and save it where future work will find it.</span>

## <span data-proof="authored" data-by="ai:claude">When to Use</span>

* <span data-proof="authored" data-by="ai:claude">After completing a plan, campaign, analysis, or strategy session</span>

* <span data-proof="authored" data-by="ai:claude">"Compound this session", "Save what we learned", "What should we remember?"</span>

* <span data-proof="authored" data-by="ai:claude">After a data correction, process fix, or strategic insight</span>

* <span data-proof="authored" data-by="ai:claude">At the end of any meaningful work session</span>

## <span data-proof="authored" data-by="ai:claude">Process</span>

### <span data-proof="authored" data-by="ai:claude">Step 1: Identify learnings</span>

<span data-proof="authored" data-by="ai:claude">Scan the current session for compoundable insights. Look for:</span>

| <span data-proof="authored" data-by="ai:claude">Type</span>           | <span data-proof="authored" data-by="ai:claude">Signals</span>                                                               |
| --------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **<span data-proof="authored" data-by="ai:claude">Insight</span>**    | <span data-proof="authored" data-by="ai:claude">"We discovered...", surprising finding, counter-intuitive result</span>      |
| **<span data-proof="authored" data-by="ai:claude">Playbook</span>**   | <span data-proof="authored" data-by="ai:claude">Repeatable process that worked, step-by-step that others could follow</span> |
| **<span data-proof="authored" data-by="ai:claude">Correction</span>** | <span data-proof="authored" data-by="ai:claude">Wrong assumption fixed, data source clarified, definition updated</span>     |
| **<span data-proof="authored" data-by="ai:claude">Pattern</span>**    | <span data-proof="authored" data-by="ai:claude">Something that keeps recurring, systemic observation</span>                  |

**<span data-proof="authored" data-by="ai:claude">Extract 1-3 learnings max.</span>** <span data-proof="authored" data-by="ai:claude">Quality over quantity. If nothing is worth saving, say so:</span>

> <span data-proof="authored" data-by="ai:claude">"Nothing from this session seems worth saving as a standalone learning. The work is captured in the plan/deliverables."</span>

<span data-proof="authored" data-by="ai:claude">For each learning, draft:</span>

```
**Learning:** [One sentence — what we now know]
**Type:** [insight | playbook | correction | pattern]
**Why it matters:** [One sentence — how this changes future work]
```

### <span data-proof="authored" data-by="ai:claude">Step 2: Get user approval</span>

<span data-proof="authored" data-by="ai:claude">Present the drafted learnings and ask:</span>

> <span data-proof="authored" data-by="ai:claude">"Found [N] learnings worth saving. Review and approve?"</span>

<span data-proof="authored" data-by="ai:claude">Show each learning with its classification. User can:</span>

* <span data-proof="authored" data-by="ai:claude">Approve as-is</span>

* <span data-proof="authored" data-by="ai:claude">Edit the wording</span>

* <span data-proof="authored" data-by="ai:claude">Skip individual learnings</span>

* <span data-proof="authored" data-by="ai:claude">Add learnings you missed</span>

**<span data-proof="authored" data-by="ai:claude">Do not save anything without approval.</span>**

### <span data-proof="authored" data-by="ai:claude">Step 3: Check for duplicates</span>

<span data-proof="authored" data-by="ai:claude">For each approved learning, search existing knowledge:</span>

```
Grep: [key phrases] in docs/knowledge/
Grep: [key phrases] in docs/solutions/
```

<span data-proof="authored" data-by="ai:claude">If a similar learning already exists:</span>

* <span data-proof="authored" data-by="ai:claude">Show the existing entry</span>

* <span data-proof="authored" data-by="ai:claude">Ask: "Update existing or save as new?"</span>

* <span data-proof="authored" data-by="ai:claude">If updating, edit the existing file</span>

### <span data-proof="authored" data-by="ai:claude">Step 4: Save locally</span>

<span data-proof="authored" data-by="ai:claude">Write each learning to</span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`:</span>

**<span data-proof="authored" data-by="ai:claude">Filename:</span>**<span data-proof="authored" data-by="ai:claude"></span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/{descriptive-slug}.md`</span>

<span data-proof="authored" data-by="ai:claude">Create the directory if it doesn't exist:</span> <span data-proof="authored" data-by="ai:claude">`mkdir -p docs/knowledge/`</span>

**<span data-proof="authored" data-by="ai:claude">File format:</span>**

```markdown proof:W3sidHlwZSI6InByb29mQXV0aG9yZWQiLCJmcm9tIjowLCJ0byI6NTQyLCJhdHRycyI6eyJieSI6ImFpOmNsYXVkZSJ9fV0=
---
type: [insight | playbook | correction | pattern]
tags: [relevant keywords for future search]
confidence: [high | medium | low]
created: [today's date]
source: [brief description of what triggered this]
---

# [Learning Title]

[2-4 sentences explaining the learning. Be specific enough that someone reading this in 3 months understands what happened and why it matters.]

## Context

[What you were doing when you discovered this.]

## Implication

[How this should change future work. Be concrete: "When doing X, always check Y first."]
```

### <span data-proof="authored" data-by="ai:claude">Step 5: Confirm and summarize</span>

```
## Compounded

**Saved:**
- docs/knowledge/{filename}.md

**This learning will be surfaced by /kw:plan** when future work touches:
- [list the tags that would trigger retrieval]
```

## <span data-proof="authored" data-by="ai:claude">Important Rules</span>

* **<span data-proof="authored" data-by="ai:claude">1-3 learnings max per session.</span>** <span data-proof="authored" data-by="ai:claude">If you're saving 5 things, you're not filtering enough.</span>

* **<span data-proof="authored" data-by="ai:claude">Approval required.</span>** <span data-proof="authored" data-by="ai:claude">Never auto-save. The user decides what's worth remembering.</span>

* **<span data-proof="authored" data-by="ai:claude">Be specific.</span>** <span data-proof="authored" data-by="ai:claude">"Use the right data source" is useless. "Revenue metrics come from [specific dashboard], not [other source] which overcounts by ~$X" is useful.</span>

* **<span data-proof="authored" data-by="ai:claude">Duplicates are waste.</span>** <span data-proof="authored" data-by="ai:claude">Always check before creating. Update existing entries when possible.</span>

* **<span data-proof="authored" data-by="ai:claude">Confidence matters.</span>** <span data-proof="authored" data-by="ai:claude">Mark</span> <span data-proof="authored" data-by="ai:claude">`low`</span> <span data-proof="authored" data-by="ai:claude">if based on one data point. Mark</span> <span data-proof="authored" data-by="ai:claude">`high`</span> <span data-proof="authored" data-by="ai:claude">if verified across multiple sessions or with data.</span>

* **<span data-proof="authored" data-by="ai:claude">Tags are for retrieval.</span>** <span data-proof="authored" data-by="ai:claude">Choose tags that</span> <span data-proof="authored" data-by="ai:claude">`/kw:plan`'s grep search would match on. Think: "What future question would this answer?"</span>