# Compound Knowledge Plugin Development

## Plugin Structure

```
compound-knowledge/
├── AGENTS.md                        # Dev conventions (this file)
├── CLAUDE.md                        # Shim → @AGENTS.md
├── skills/                          # 7 workflow skills
│   ├── kw-brainstorm/SKILL.md
│   ├── kw-plan/SKILL.md
│   ├── kw-confidence/SKILL.md
│   ├── kw-review/SKILL.md
│   ├── kw-work/SKILL.md
│   ├── kw-compound/SKILL.md
│   └── kw-lfg/SKILL.md              # Hands-off loop (plan → review → work → compound)
├── agents/                          # 5 task agents
│   ├── review/
│   │   ├── strategic-alignment-reviewer.md
│   │   └── data-accuracy-reviewer.md
│   └── research/
│       ├── knowledge-base-researcher.md
│       ├── past-work-researcher.md
│       └── stale-knowledge-checker.md
├── README.md
├── CHANGELOG.md
├── PRIVACY.md
├── SECURITY.md
└── LICENSE
```

## Conventions

* Workflow skills live in `skills/{skill-name}/SKILL.md`

* Each skill has YAML frontmatter with `name:`, `description:`, and optionally `argument-hint:`

* Skills use `kw:` prefix (e.g., `/kw:brainstorm`)

* Skills that accept arguments include an XML capture tag after frontmatter (e.g., `<brain_dump> #$ARGUMENTS </brain_dump>`)

* End-of-stage handoffs must (1) name the completed stage, (2) present next options, and (3) immediately load the chosen next skill when applicable — never silently skip the handoff

* Handoff menus: Claude Code `AskUserQuestion` max 4 options — if more are visible, use a numbered list in chat instead of overloading the tool

* `/kw:lfg` is the only skill that chains stages without check-ins; it invokes children with `mode:pipeline`. Other skills stay single-stage unless the user picks a handoff option; under `mode:pipeline` they return results to the caller and do not self-chain

* Review agents live in `agents/review/`

* Research agents live in `agents/research/`

## Versioning

Every change must update:

1. `.claude-plugin/plugin.json` version
2. `CHANGELOG.md`
3. `README.md` component counts (if changed)

## Design Principles

* **Generic over specific.** No company-specific references in workflow skills. Project context comes from the user's CLAUDE.md.

* **Opinionated but adaptable.** The workflows have strong defaults (Pyramid Principle, P1/P2/P3 severity) but adapt to whatever project they're installed in.

* **Local first.** `docs/knowledge/` is the primary knowledge store. External integrations (Notion, etc.) are optional and project-specific.

* **Progressive disclosure.** Start with the core workflows. Add skills and agents as patterns emerge. `/kw:lfg` is the autonomous path for users who already trust the loop.

* **Stage clarity.** Users should always know whether they are in brainstorm, plan, review, work, or compound.
