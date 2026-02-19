---
name: workflows:review
description: Multi-reviewer quality check for knowledge work. Runs strategic alignment and data accuracy reviewers on plans, briefs, and strategy docs.
---

# Review

Two automated reviewers check your work for the errors that damage credibility: wrong strategy and wrong data.

## When to Use

* After `/workflows:plan` to validate a plan before executing

* Before sharing a strategy doc, brief, or analysis with stakeholders

* "Review this plan", "Check this brief", "Is the data right?"

* Any knowledge work artifact that will be seen by decision-makers

## What Gets Reviewed

The most recently produced artifact. Determined by context:

| Situation                  | What to review                                                         |
| -------------------------- | ---------------------------------------------------------------------- |
| `/workflows:plan` just ran | The plan file it produced                                              |
| User points to a file      | That file                                                              |
| User pastes content        | That content                                                           |
| Ambiguous                  | Ask: "What should I review? Provide a file path or paste the content." |

## Process

### Step 1: Load the content

Read the file or accept pasted content. If the content references data (metrics, conversion rates, financial figures), also load:

* Any data context files referenced in the project's CLAUDE.md

* Check freshness of any data files cited

### Step 2: Run Strategic Alignment Review

Apply this checklist to the content:

**Focus:** Does this serve the stated goals? Is the hypothesis grounded? Are we solving the right problem?

**Checklist:**

* [ ] Goal is explicit and connected to a measurable outcome

* [ ] Hypothesis is falsifiable ("If X, then Y will change by Z")

* [ ] Success metrics are defined and measurable

* [ ] Scope is proportional to expected impact (don't build a platform for a one-off)

* [ ] No vanity metrics (impressions without conversion, engagement without attribution)

* [ ] Resources required are stated

* [ ] Consistent with stated company/team goals (check CLAUDE.md if available)

**References to check:**

* Business context from CLAUDE.md (if available)

* Recent plans in `plans/` for consistency

* `docs/knowledge/` for past strategic learnings

**Output per finding:**

```
[P1|P2|P3] [Strategic]: [Description of the issue]
  → Suggestion: [How to fix it]
```

### Step 3: Run Data Accuracy Review

Apply this checklist to the content:

**Focus:** Are the numbers right? Are the sources cited? Would this survive a stakeholder asking "where'd you get that?"

**Checklist:**

* [ ] Every number has a source (dashboard name, file, API endpoint)

* [ ] Comparison baselines are explicit ("+32% vs what?" — WoW, MoM, YTD average)

* [ ] Numbers match canonical definitions (if the project has a data context file)

* [ ] Data is fresh — flag anything older than 48 hours as potentially stale

* [ ] Known caveats are acknowledged

* [ ] No hardcoded numbers that should be live-queried

* [ ] Comparisons use appropriate baselines (watch for weekend/seasonal skew)

**Output per finding:**

```
[P1|P2|P3] [Data]: [Description of the issue]
  → Source should be: [correct source]
  → Current value: [if verifiable]
```

### Step 4: Run editorial check (if external-facing)

If the content will be published, emailed, or posted publicly:

* Check for AI writing patterns (generic phrasing, stock transitions, vague claims)

* Check tone and voice consistency with project style guides

If the content is internal (plan, brief, analysis for the team): skip this step.

### Step 5: Present findings

Group all findings by severity:

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

| Severity            | What qualifies                                                           | Examples                                        |
| ------------------- | ------------------------------------------------------------------------ | ----------------------------------------------- |
| **P1 Critical**     | Factual error, wrong data source, missing goal, unfalsifiable hypothesis | "Metric cited from wrong source"                |
| **P2 Important**    | Missing source citation, stale data, unclear success metric              | "Conversion rate has no comparison basis"       |
| **P3 Nice-to-have** | Minor framing, additional context, formatting                            | "Could specify the time period for this metric" |

### Step 6: Offer next steps

Use AskUserQuestion:

**Question:** "Review complete. \[N] findings (\[P1 count] critical, \[P2 count] important). What next?"

**Options:**

1. **Fix P1/P2 issues now** — Address findings inline
2. **Re-review after fixes** — Run the review again on updated content
3. **Run** **`/workflows:compound`** — Save review insights as learnings
4. **Ship as-is** — Acknowledge findings and proceed

## Important Rules

* **P1 = hard gate.** A factual error in a strategy doc is worse than a typo. Say so clearly.

* **Verify, don't assume.** If a number is cited, check it against the actual source if possible. Don't just check formatting.

* **Flag staleness.** Data older than 48 hours gets a freshness warning. Data older than 7 days gets a P2.

* **Be specific.** "Data might be wrong" is not useful. "Revenue cited as $X but source shows $Y as of \[date]" is.

* **Credit what's good.** Don't only flag problems. Note sections that are well-grounded and clearly structured.