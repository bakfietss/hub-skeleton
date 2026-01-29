# Agent Collaboration Guide

## Structuur

```
.claude/agents/
├── core/                    # ALTIJD beschikbaar
│   ├── api-architect.md     # ALLE API werk
│   ├── code-reviewer.md     # QA, security, best practices
│   ├── task-manager.md      # Planning, prioritering
│   └── docs-manager.md      # CHANGELOG, documentatie
│
├── infra/                   # Deployment & automation (optioneel)
│   ├── docker-specialist.md # Containers, compose
│   └── n8n-specialist.md    # Workflows, automation
│
├── [project]/               # Project-specifieke agents
│   └── ...
│
└── gsd/                     # GSD interne agents
    └── (automatisch door GSD)
```

## Wanneer Welke Agents

### Core Agents (altijd beschikbaar)
| Agent | Gebruik |
|-------|---------|
| `api-architect` | **ALLE API werk** - endpoints, validation, error handling |
| `code-reviewer` | Voor deployment, na grote changes, security check |
| `task-manager` | Project planning, prioritering, tracking |
| `docs-manager` | CHANGELOG updates, documentatie |

### Infra Agents (na installatie)
| Agent | Gebruik |
|-------|---------|
| `docker-specialist` | Container setup, deployment configs |
| `n8n-specialist` | Workflow building, n8n configuratie |

## Workflow

```
┌─────────────────────────────────────────────────────────┐
│  ALTIJD VANUIT HUB ROOT WERKEN                          │
│  cd /path/to/hub                                        │
└─────────────────────────────────────────────────────────┘
                          │
         ┌────────────────┼────────────────┐
         ▼                ▼                ▼
   ┌──────────┐    ┌──────────┐    ┌──────────┐
   │ Solution │    │ Solution │    │ Klant    │
   │ A        │    │ B        │    │ Project  │
   └──────────┘    └──────────┘    └──────────┘
         │                │                │
         ▼                ▼                ▼
   core + project   core + project   core + infra
   agents           agents           agents
```

## Agent Aanroep Patronen

### Bij algemeen development:
1. `task-manager` → plan het werk
2. `api-architect` → API design (indien API)
3. [project-specific agent] → implementatie
4. `code-reviewer` → check voor completion
5. `docs-manager` → update CHANGELOG

### Bij deployment:
1. `task-manager` → plan het werk
2. `docker-specialist` → maak configs (indien nodig)
3. `n8n-specialist` → bouw workflows (indien nodig)
4. `code-reviewer` → check voor deployment
5. `docs-manager` → update CHANGELOG

### Bij API development:
1. `task-manager` → plan het werk
2. `api-architect` → **design & implementatie**
3. `code-reviewer` → security & QA check
4. `docs-manager` → update CHANGELOG

## Regels

1. **Altijd vanuit hub root werken** - Niet vanuit subdirectories
2. **Core agents zijn altijd relevant** - Gebruik ze bij elk project
3. **Project agents alleen voor dat project** - Niet mengen
4. **Code-reviewer voor deployment** - Altijd QA check doen
5. **Docs-manager na changes** - CHANGELOG bijhouden

## Agents Toevoegen

Zie `REGISTRY.md` voor:
- Decision tree voor categorisatie
- Checklist voor nieuwe agents
- Agent template
