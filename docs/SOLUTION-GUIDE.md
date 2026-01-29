# Solution Guide

> Hoe je nieuwe solutions aanmaakt en beheert

---

## Wat is een Solution?

Een solution is een standalone product of project binnen de hub. Voorbeelden:
- Web applicatie
- API service
- Automation tool
- Client project

---

## Verplichte Structuur

**ELKE solution MOET deze structuur hebben:**

```
solutions/[naam]/
├── .planning/              ← VERPLICHT
│   ├── PROJECT.md          ← Vision, problem, solution
│   ├── STATE.md            ← Todo list, huidige status
│   ├── BACKLOG.md          ← Gedetailleerde tasks
│   └── ROADMAP.md          ← Fase planning
│
├── agents/                 ← VERPLICHT
│   └── README.md           ← Welke agents, configuratie
│
├── CLAUDE.md               ← Entry point voor Claude
├── README.md               ← Project overview
│
├── src/                    ← Source code (optioneel)
├── config/                 ← Configuratie (optioneel)
└── docs/                   ← Solution docs (optioneel)
```

---

## Nieuwe Solution Aanmaken

### Stap 1: Folders maken

```bash
mkdir -p solutions/my-solution/.planning
mkdir -p solutions/my-solution/agents
mkdir -p solutions/my-solution/src
```

### Stap 2: Planning bestanden

**`.planning/PROJECT.md`**
```markdown
# [Solution Naam]

## Problem Statement
Welk probleem lost dit op?

## Solution
Hoe lossen we het op?

## Success Criteria
Wanneer is het klaar?

## Tech Stack
- Technology 1
- Technology 2
```

**`.planning/STATE.md`**
```markdown
# [Solution] - Current State

## Status
🟡 In Development

## Current Sprint
- [ ] Taak 1
- [ ] Taak 2

## Blockers
Geen

## Next Steps
1. Volgende stap
```

**`.planning/ROADMAP.md`**
```markdown
# [Solution] Roadmap

## Phase 1: Foundation
- [ ] Setup project
- [ ] Basic structure

## Phase 2: Core Features
- [ ] Feature A
- [ ] Feature B

## Phase 3: Polish
- [ ] Testing
- [ ] Documentation
```

### Stap 3: Agent configuratie

**`agents/README.md`**
```markdown
# Agents voor [Solution]

## Core Agents (altijd)
- code-reviewer
- task-manager
- docs-manager

## Project-Specifieke Agents
- [Indien nodig, voeg toe aan .claude/agents/[solution-naam]/]

## Configuratie
[Eventuele speciale instellingen]
```

### Stap 4: Entry points

**`CLAUDE.md`**
```markdown
# [Solution Name]

## Quick Start
```bash
cat .planning/STATE.md
```

## Tech Stack
- Tech 1
- Tech 2

## Key Commands
[Relevante commando's]
```

**`README.md`**
```markdown
# [Solution Name]

> Korte beschrijving

## Features
- Feature 1
- Feature 2

## Installation
[Setup instructies]

## Usage
[Hoe te gebruiken]
```

---

## Checklist Nieuwe Solution

- [ ] `.planning/PROJECT.md` aangemaakt
- [ ] `.planning/STATE.md` aangemaakt
- [ ] `.planning/BACKLOG.md` aangemaakt
- [ ] `.planning/ROADMAP.md` aangemaakt
- [ ] `agents/README.md` aangemaakt
- [ ] `CLAUDE.md` aangemaakt
- [ ] `README.md` aangemaakt
- [ ] Eerste commit gedaan

---

## Solution Werken

### Vanuit Hub Root

```bash
# Altijd vanuit hub root werken
cd /path/to/hub
claude

# Specificeer solution in je vraag:
"In solutions/my-solution, voeg feature X toe"
```

### GSD Gebruiken

```bash
# Start met de solution context
/gsd:progress
# Kies de solution als gevraagd
```

---

## Project-Specifieke Agents

Als je solution specifieke agents nodig heeft:

### 1. Maak agent folder

```bash
mkdir -p .claude/agents/[solution-naam]
```

### 2. Voeg agent toe

```markdown
# [Naam] Specialist

## Expertise
- Skill 1
- Skill 2

## Tools
- Read, Write, Edit, Bash, Grep, Glob

## Wanneer Gebruiken
- Situatie 1
- Situatie 2
```

### 3. Update REGISTRY.md

Voeg toe aan `.claude/agents/REGISTRY.md`

---

## Tips

### Structuur
- Houd structuur consistent
- Documenteer altijd de tech stack
- Update STATE.md elke sessie

### Development
- Kleine, frequent commits
- Code review voor merge
- Test lokaal voor deploy

### Planning
- Gebruik GSD voor grote features
- Break down in kleine taken
- Track blockers in STATE.md

---

*Consistent structuur = Consistent succes*
