# Hub Skeleton

> Template voor het opzetten van een AI-gestuurde project management hub

## Wat is dit?

Hub Skeleton is een complete template voor het opzetten van een gecentraliseerde development hub met:

- **GSD Framework** - Get Shit Done project management
- **Agent System** - Gespecialiseerde AI assistenten
- **Consistent Structure** - Templates voor solutions en projecten
- **Modulaire Opzet** - Core + optional modules

## Features

- 4 Core agents (code-reviewer, task-manager, api-architect, docs-manager)
- GSD framework voor project management
- Templates voor solutions en projecten
- Modulaire architectuur voor uitbreidingen
- Documentatie en guides

## Quick Start

```bash
# 1. Clone en reset
git clone https://github.com/[user]/hub-skeleton.git my-hub
cd my-hub
rm -rf .git
git init

# 2. Pas aan
# Edit CLAUDE.md met jouw hub naam
# Edit .planning/PROJECT.md

# 3. Start
git add .
git commit -m "[FEAT] Initial hub setup"

# 4. Begin met Claude
claude
/gsd:progress
```

## Structure

```
hub-skeleton/
├── .claude/              ← Agents & framework
│   ├── agents/           ← Core agents
│   ├── commands/gsd/     ← GSD commands
│   └── get-shit-done/    ← GSD framework
├── .planning/            ← Hub planning
├── docs/                 ← Documentation
├── deploy/templates/     ← Project templates
├── solutions/            ← Your solutions
├── klanten/              ← Client projects
└── personal/             ← Experiments
```

## Documentation

- [Installation Guide](docs/INSTALLATION.md)
- [Daily Workflow](docs/WORKFLOW.md)
- [Solution Guide](docs/SOLUTION-GUIDE.md)
- [GSD Guide](docs/GSD-GUIDE.md)
- [Agent Guide](docs/AGENT-GUIDE.md)

## Optional Modules

Install extra capabilities as needed:

| Module | Purpose |
|--------|---------|
| n8n | Workflow automation agent + skills |
| docker | Container management agent |
| [custom] | Add your own agents |

See [INSTALLATION.md](docs/INSTALLATION.md) for setup instructions.

## License

MIT

## Contributing

Feel free to submit issues and PRs.
