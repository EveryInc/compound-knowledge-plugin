# <span data-proof="authored" data-by="ai:claude">Compound Knowledge Plugin Development</span>

## <span data-proof="authored" data-by="ai:claude">Plugin Structure</span>

```
compound-knowledge/
├── .claude-plugin/plugin.json    # Plugin manifest
├── commands/workflows/           # 5 workflow commands
├── agents/review/                # Review agents
├── skills/                       # Topic skills (future)
├── README.md
├── CLAUDE.md
├── CHANGELOG.md
└── LICENSE
```

## <span data-proof="authored" data-by="ai:claude">Conventions</span>

* <span data-proof="authored" data-by="ai:claude">Workflow commands live in</span> <span data-proof="authored" data-by="ai:claude">`commands/workflows/`</span>

* <span data-proof="authored" data-by="ai:claude">Each command has YAML frontmatter with</span> <span data-proof="authored" data-by="ai:claude">`name:`</span> <span data-proof="authored" data-by="ai:claude">and</span> <span data-proof="authored" data-by="ai:claude">`description:`</span>

* <span data-proof="authored" data-by="ai:claude">Commands use</span> <span data-proof="authored" data-by="ai:claude">`workflows:`</span> <span data-proof="authored" data-by="ai:claude">prefix (e.g.,</span> <span data-proof="authored" data-by="ai:claude">`/workflows:brainstorm`)</span>

* <span data-proof="authored" data-by="ai:claude">Review agents live in</span> <span data-proof="authored" data-by="ai:claude">`agents/review/`</span>

* <span data-proof="authored" data-by="ai:claude">Skills live in</span> <span data-proof="authored" data-by="ai:claude">`skills/{skill-name}/SKILL.md`</span>

## <span data-proof="authored" data-by="ai:claude">Versioning</span>

<span data-proof="authored" data-by="ai:claude">Every change must update:</span>

1. <span data-proof="authored" data-by="ai:claude">`.claude-plugin/plugin.json`</span> <span data-proof="authored" data-by="ai:claude">version</span>
2. <span data-proof="authored" data-by="ai:claude">`CHANGELOG.md`</span>
3. <span data-proof="authored" data-by="ai:claude">`README.md`</span> <span data-proof="authored" data-by="ai:claude">component counts (if changed)</span>

## <span data-proof="authored" data-by="ai:claude">Design Principles</span>

* **<span data-proof="authored" data-by="ai:claude">Generic over specific.</span>** <span data-proof="authored" data-by="ai:claude">No company-specific references in workflow commands. Project context comes from the user's CLAUDE.md.</span>

* **<span data-proof="authored" data-by="ai:claude">Opinionated but adaptable.</span>** <span data-proof="authored" data-by="ai:claude">The workflows have strong defaults (Pyramid Principle, P1/P2/P3 severity) but adapt to whatever project they're installed in.</span>

* **<span data-proof="authored" data-by="ai:claude">Local first.</span>**<span data-proof="authored" data-by="ai:claude"></span> <span data-proof="authored" data-by="ai:claude">`docs/knowledge/`</span> <span data-proof="authored" data-by="ai:claude">is the primary knowledge store. External integrations (Notion, etc.) are optional and project-specific.</span>

* **<span data-proof="authored" data-by="ai:claude">Progressive disclosure.</span>** <span data-proof="authored" data-by="ai:claude">Start with the 5 workflows. Add skills and agents as patterns emerge.</span>