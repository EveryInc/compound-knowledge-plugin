---
name: kw:review
description: Multi-reviewer quality check for knowledge work. Runs strategic alignment and data accuracy reviewers on plans, briefs, and strategy docs.
---

# Review

Two automated reviewers check your work for the errors that damage credibility: wrong strategy and wrong data.

## When to Use

* After `/kw:plan` to validate a plan before executing

* Before sharing a strategy doc, brief, or analysis with stakeholders

* "Review this plan", "Check this brief", "Is the data right?"

* Any knowledge work artifact that will be seen by decision-makers

## What Gets Reviewed

The most recently produced artifact. Determined by context:

| Situation             | What to review                                                         |
| --------------------- | ---------------------------------------------------------------------- |
| `/kw:plan` just ran   | The plan file it produced                                              |
| User points to a file | That file                                                              |
| User pastes content   | That content                                                           |
| Ambiguous             | Ask: "What should I review? Provide a file path or paste the content." |

## Process

### Step 1: Load the content

Read the file or accept pasted content. If the content references data (metrics, conversion rates, financial figures), also load:

* Any data context files referenced in the project's CLAUDE.md

* Check freshness of any data files cited

### Step 2: Run both reviewers in parallel

Launch **both** reviewers simultaneously as Task agents. They are independent — neither needs the other's output.

**Launch in parallel:**

1. **Strategic Alignment Reviewer** (Task agent: `strategic-alignment-reviewer`)

   * Pass: the full content + any business context from CLAUDE.md

   * It checks: goal clarity, falsifiable hypothesis, success metrics, scope proportionality, resource awareness, strategic consistency

2. **Data Accuracy Reviewer** (Task agent: `data-accuracy-reviewer`)

   * Pass: the full content + any data context files referenced in CLAUDE.md

   * It checks: source citations, comparison baselines, canonical definitions, freshness, caveats, hardcoded numbers

**Both agents return findings in** **`[P1|P2|P3]`** **format.** Wait for both to complete before proceeding.

### Step 3: Run editorial check (if external-facing)

If the content will be published, emailed, or posted publicly:

* Check for AI writing patterns (generic phrasing, stock transitions, vague claims)

* Check tone and voice consistency with project style guides

If the content is internal (plan, brief, analysis for the team): skip this step.

### Step 4: Merge and present findings

Combine findings from both reviewers. Group all findings by severity:

```
## Review: [Document Title]

### P1 — Blocks Shipping
[These must be fixed before sharing. Wrong data, wrong goal, unfalsifiable hypothesis.]

### P2 — Should Fix
[Important but not blocking. Missing sources, unclear metrics, scope concerns.]

### P3 — Nice to Have
[Minor refinements. Wording, additional context, formatting.]

### Clean
[Sections that passed all checks — explicitly note what's good.]
```

**Severity definitions:**

| <span data-proof="authored" data-by="ai:claude">Severity</span>         | What qualifies                                                                                                                  | <span data-proof="authored" data-by="ai:claude">Examples</span>                                  |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **<span data-proof="authored" data-by="ai:claude">P1 Critical</span>**  | <span data-proof="authored" data-by="ai:claude">Factual error, wrong data source, missing goal, unfalsifiable hypothesis</span> | "Metric cited from wrong source"                                                                 |
| **<span data-proof="authored" data-by="ai:claude">P2 Important</span>** | <span data-proof="authored" data-by="ai:claude">Missing source citation, stale data, unclear success metric</span>              | <span data-proof="authored" data-by="ai:claude">"Conversion rate has no comparison basis"</span> |
| **P3 Nice-to-have**                                                     | <span data-proof="authored" data-by="ai:claude">Minor framing, additional context, formatting</span>                            | "Could specify the time period for this metric"                                                  |

### Step 5: Offer next steps

Use AskUserQuestion:

**Question:** "Review complete. \[N] findings (\[P1 count] critical, \[P2 count] important). What next?"

**Options:**

1. **Fix P1/P2 issues now** — Address findings inline, then re-review
2. **Run `/kw:work`** — Plan passes. Start executing it
3. **Run `/kw:compound`** — Save review insights as learnings
4. **Ship as-is** — Acknowledge findings and proceed without fixing

## Important Rules

* **P1 = hard gate.** A factual error in a strategy doc is worse than a typo. Say so clearly.

* **Verify, don't assume.** If a number is cited, check it against the actual source if possible. Don't just check formatting.

* **Flag staleness.** Data older than 48 hours gets a freshness warning. Data older than 7 days gets a P2.

* **Be specific.** "Data might be wrong" is not useful. "Revenue cited as $X but source shows $Y as of \[date]" is.

* **Credit what's good.** Don't only flag problems. Note sections that are well-grounded and clearly structured.