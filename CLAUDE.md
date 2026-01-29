# [Hub Name]

> Centrale hub voor AI-gestuurde project management

---

## ALTIJD HIER STARTEN

```bash
# Elke sessie:
/gsd:progress

# Of handmatig:
cat .planning/STATE.md
```

**Documentatie:** [`docs/INDEX.md`](docs/INDEX.md) - Centrale index

---

## Project Structuur

```
hub/
├── .claude/                    ← Agents, skills, commands (IP)
├── .planning/                  ← Hub-level planning
│   ├── STATE.md                ← ⭐ ALTIJD LEZEN
│   ├── BACKLOG.md              ← Open items
│   └── ROADMAP.md              ← Milestones
│
├── solutions/                  ← Product development
│   └── [solution-name]/        ← Individuele solutions
│
├── klanten/                    ← Klant projecten (gitignored)
├── personal/                   ← Experimenten
├── deploy/templates/           ← Project templates
└── docs/                       ← Documentatie
```

---

## Belangrijke Conventies

### Git Commits
```
[FEAT] nieuwe feature     → Added
[FIX] bug fix             → Fixed
[DOCS] documentatie       → Documentation
[REFACTOR] code opschonen → Refactored
[CHORE] maintenance       → Changed
[WIP] work in progress    → Skip changelog
```

### Nieuwe Solution Aanmaken

**Bij ELKE nieuwe solution MOET je deze structuur aanmaken:**

```
solutions/[naam]/
├── .planning/              ← VERPLICHT
│   ├── PROJECT.md
│   ├── STATE.md
│   ├── BACKLOG.md
│   └── ROADMAP.md
├── agents/                 ← VERPLICHT
│   └── README.md
├── CLAUDE.md
└── README.md
```

**NOOIT een solution starten zonder volledige structuur.**

---

## Quick Commands

```bash
# Huidige status
cat .planning/STATE.md

# GSD progress
/gsd:progress

# Nieuwe solution maken
# Gebruik deploy/templates/solution-skeleton als basis
```

---

## Installatie Modules

De hub heeft core functionaliteit standaard. Extra modules installeren:

| Module | Wat | Hoe |
|--------|-----|-----|
| n8n | Workflow automation | Zie docs/INSTALLATION.md |
| docker | Container management | Zie docs/INSTALLATION.md |

---

*Zie `docs/INDEX.md` voor volledige documentatie*
