# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [1.1.0] - 2026-08-31

### Added

* `/kw:lfg` — Hands-off loop runner (plan → review → work → compound), the knowledge-work counterpart to Compound Engineering's `/lfg`
* Stage orientation banners on all workflow skills (`**Stage: …**`) so mid-conversation it stays clear which phase you're in
* Mandatory end-of-stage handoff menus that recommend the next skill and, when chosen, immediately load it (instead of only suggesting the user type the command)
* Brainstorm / plan handoff option: **Ship the loop with `/kw:lfg`**

### Changed

* `/kw:brainstorm` Step 7 reframed as an explicit "Brainstorm complete" handoff (never skip), aligned with CE's post-brainstorm progression
* `/kw:plan`, `/kw:review`, `/kw:work`, and `/kw:compound` handoffs strengthened with stage-complete preambles and immediate skill load on selection
* Handoff menus follow CE's AskUserQuestion cap: ≤4 options use the tool; more than 4 fall back to a numbered list (never call AskUserQuestion over the limit)
* Pipeline Mode now keys off `mode:pipeline` (not `disable-model-invocation`); children return results to the caller instead of self-chaining
* `/kw:compound` allows pipeline auto-save so `/kw:lfg` does not contradict "approval required"
* LFG option labeled **Ship the rest**; existing `plans/*.md` paths skip re-planning; work end option renamed **Done for now**
* `/kw:confidence` captures and resumes the interrupted parent stage
* README / component counts updated for 7 skills

## [1.0.0] - 2026-03-22

### Added

* 3 research agents: past-work-researcher, knowledge-base-researcher, stale-knowledge-checker
* Parallel research agent architecture in `/kw:plan` — launches agents instead of inline grep
* Auto-search in `/kw:brainstorm` — knowledge base and past plans searched automatically
* Stale knowledge detection in `/kw:compound` — flags contradictions before saving
* Origin document chain — brainstorms become origin docs that plans reference and cross-check
* Detail tiers in `/kw:plan` — Quick, Standard, Deep based on scope signals
* Execution log persistence in `/kw:work` — appends to plan file, not just conversation
* Proof integration — "Push to Proof" offered at all handoff points
* Pipeline mode for all 6 skills — supports autonomous chaining
* PRIVACY.md and SECURITY.md

### Changed

* Migrated from `commands/kw/` to `skills/kw-*/SKILL.md` structure
* Added `$ARGUMENTS` capture and `argument-hint` frontmatter to skills
* Review agents now referenced by fully-qualified names
* Updated "Lead with the answer" rule to be work-type-specific
* CLAUDE.md is now a shim to AGENTS.md (matching compound-engineering convention)
* README split: root is landing page, plugin README is full reference

## [0.2.0] - 2026-02-23

### Added

* `/kw:confidence` — Gut-check what you know and don't know before proceeding. Plain-language confidence assessment with actionable steps to resolve gaps.

## [0.1.0] - 2026-02-19

### Added

* `/kw:brainstorm` — Brain dump and compile knowledge before planning

* `/kw:plan` — Research past work and structure actionable plans

* `/kw:review` — Strategic alignment + data accuracy review (P1/P2/P3)

* `/kw:work` — Execute plans with task tracking

* `/kw:compound` — Save learnings to `docs/knowledge/`

* Strategic alignment reviewer agent

* Data accuracy reviewer agent

* README with install and usage instructions
