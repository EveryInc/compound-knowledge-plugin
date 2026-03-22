# Compound Knowledge Plugin Development

## Plugin Structure

```
compound-knowledge/
├── AGENTS.md                        # Dev conventions (this file)
├── CLAUDE.md                        # Shim → @AGENTS.md
├── skills/                          # 6 workflow skills
│   ├── kw-brainstorm/SKILL.md
│   ├── kw-plan/SKILL.md
│   ├── kw-confidence/SKILL.md
│   ├── kw-review/SKILL.md
│   ├── kw-work/SKILL.md
│   └── kw-compound/SKILL.md
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

* **Progressive disclosure.** Start with the 6 workflows. Add skills and agents as patterns emerge.
