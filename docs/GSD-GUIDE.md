# GSD Framework Guide

> Get Shit Done - Project Management met Claude

---

## Wat is GSD?

GSD (Get Shit Done) is een framework voor gestructureerd project management met Claude. Het biedt:

- **Consistente planning** via templates
- **Tracking** via STATE.md
- **Workflows** voor development cycli
- **Commands** voor snelle acties

---

## Core Concepts

### Hiërarchie

```
Project
└── Milestone (grote doelen)
    └── Phase (groep taken)
        └── Task (individueel werk)
```

### Key Files

| File | Doel |
|------|------|
| `PROJECT.md` | Vision, scope, success criteria |
| `STATE.md` | Huidige status, actieve taken |
| `ROADMAP.md` | Milestones en fases |
| `BACKLOG.md` | Alle open items |

---

## Basis Commands

### Status & Navigatie

```bash
/gsd:progress      # Waar ben ik? Wat nu?
/gsd:help          # Alle beschikbare commands
```

### Project Lifecycle

```bash
/gsd:new-project       # Start nieuw project
/gsd:new-milestone     # Nieuwe milestone
/gsd:complete-milestone # Milestone afronden
```

### Fase Management

```bash
/gsd:create-roadmap    # Maak fase planning
/gsd:plan-phase        # Plan specifieke fase
/gsd:execute-phase     # Voer fase uit
/gsd:add-phase         # Voeg fase toe
```

### Onderzoek & Planning

```bash
/gsd:research-phase    # Research voor fase
/gsd:discuss-phase     # Bespreek aanpak
/gsd:define-requirements # Requirements vastleggen
```

### Dagelijks Werk

```bash
/gsd:check-todos       # Bekijk open taken
/gsd:add-todo          # Voeg todo toe
/gsd:verify-work       # Valideer werk
```

### Debugging

```bash
/gsd:debug             # Systematisch debuggen
/gsd:map-codebase      # Analyseer codebase
```

---

## Typische Workflow

### Nieuw Project

```bash
# 1. Start project
/gsd:new-project
# Beantwoord vragen over vision, scope, etc.

# 2. Maak roadmap
/gsd:create-roadmap
# Definieert fases en milestones

# 3. Start eerste fase
/gsd:plan-phase
# Maakt gedetailleerd plan

# 4. Uitvoeren
/gsd:execute-phase
# Voert plan stap voor stap uit
```

### Dagelijks Werk

```bash
# 1. Check status
/gsd:progress

# 2. Werk aan taken
# ... development ...

# 3. Verify werk
/gsd:verify-work

# 4. Update status
# STATE.md wordt automatisch bijgewerkt
```

### Bug Fixing

```bash
# 1. Start debug sessie
/gsd:debug

# 2. Volg hypothese-test cycle
# Framework houdt state bij

# 3. Documenteer oplossing
# Wordt opgeslagen voor later
```

---

## STATE.md Template

```markdown
# [Project] - Current State

## Quick Status
🟢 On Track / 🟡 Needs Attention / 🔴 Blocked

## Active Phase
Phase X: [naam]

## Current Sprint
- [ ] Task 1
- [ ] Task 2
- [x] Task 3 (completed)

## Blockers
- Blocker 1 (indien aanwezig)

## Decisions Made
- Decision 1: [rationale]

## Next Session
1. Eerste prioriteit
2. Tweede prioriteit
```

---

## ROADMAP.md Template

```markdown
# [Project] Roadmap

## Milestone 1: [naam]
Target: [datum]

### Phase 1.1: Foundation
- [ ] Task A
- [ ] Task B

### Phase 1.2: Core
- [ ] Task C
- [ ] Task D

## Milestone 2: [naam]
Target: [datum]

### Phase 2.1: Features
- [ ] Task E
```

---

## Tips

### Effectief Gebruik
- Begin ELKE sessie met `/gsd:progress`
- Houd STATE.md actueel
- Gebruik fases voor gegroepeerd werk
- Documenteer beslissingen

### Veelgemaakte Fouten
- Te grote fases (break down!)
- STATE.md niet updaten
- Geen requirements definiëren
- Debugging zonder hypothese

### Best Practices
- Kleine, testbare fases
- Clear acceptance criteria
- Regelmatige verify cycles
- Documenteer wat je leert

---

## GSD Agents

Het framework heeft interne agents (in `.claude/agents/gsd/`):

| Agent | Doel |
|-------|------|
| gsd-executor | Voert plannen uit |
| gsd-verifier | Verifieert werk |
| gsd-researcher | Research taken |
| gsd-debugger | Debug sessies |
| gsd-codebase-mapper | Codebase analyse |

Deze worden automatisch aangeroepen - niet handmatig gebruiken.

---

## Troubleshooting

### Command werkt niet
- Check of `.claude/commands/gsd/` bestaat
- Check of `.claude/get-shit-done/` bestaat

### STATE.md niet gevonden
- Check of `.planning/` folder bestaat
- Run `/gsd:new-project` om te initialiseren

### Context verloren
- Lees `.planning/STATE.md`
- Run `/gsd:progress`

---

*GSD maakt projecten beheersbaar - gebruik het!*
