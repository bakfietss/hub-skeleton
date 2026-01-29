# GSD Framework - Get Shit Done

> Het workflow framework voor gestructureerd project management

---

## Wat is GSD?

GSD is een task management en planning systeem voor AI-assisted development. Het zorgt voor:

1. **Persistent Memory** - Context blijft behouden tussen sessies
2. **Gestructureerd Werken** - Duidelijke fases en taken
3. **Traceerbaarheid** - Alles wordt gedocumenteerd

---

## Twee Werkwijzen

| Werkwijze | Wanneer | STATE.md Template |
|-----------|---------|-------------------|
| **Sprint/Todo** | Onderhoud, bugfixes, ad-hoc werk | `state-todo.md` |
| **Volledige GSD** | Nieuwe projecten, grote features | `state.md` |

### Sprint/Todo Werkwijze (Aanbevolen voor dagelijks werk)

```
STATE.md = Todo lijst + sessie context
BACKLOG.md = Gedetailleerde TASK specs

Sessie:
1. "Wat staat er op de todo?"
2. "Ik pak TASK-042"
3. Werk
4. "TASK-042 is klaar"
```

### Volledige GSD (Voor grote features)

```
STATE.md = Phase tracking + velocity
ROADMAP.md = Phases met deliverables

Sessie:
1. /gsd:progress
2. /gsd:plan-phase
3. /gsd:execute-plan
4. /gsd:verify-work
```

---

## Core Principe

```
STATE.md = Persistent Memory

Elke sessie:
1. Lees STATE.md (of /gsd:progress)
2. Werk
3. Update STATE.md
```

---

## Essentiële Bestanden

| Bestand | Doel | Wie Update |
|---------|------|------------|
| `STATE.md` | **Waar zijn we nu?** Huidige status, beslissingen, blockers | Na elke sessie |
| `PROJECT.md` | Wat is dit project? Vision, scope, constraints | Bij start |
| `ROADMAP.md` | Welke fases? Progress per milestone | Bij fase transitions |
| `BACKLOG.md` | Wat staat open? Bugs, features, ideas | Continue |
| `config.json` | GSD instellingen | Eenmalig |
| `README.md` | Hoe werkt deze folder? | Eenmalig |

---

## Folder Structuur

```
.planning/
├── README.md           # Uitleg (dit kopiëren)
├── PROJECT.md          # Vision & scope
├── ROADMAP.md          # Fases & milestones
├── STATE.md            # SLEUTEL - persistent memory
├── BACKLOG.md          # Open items
├── config.json         # GSD config
│
├── codebase/           # (Optioneel) Code analyse
│   ├── ARCHITECTURE.md
│   ├── STACK.md
│   └── ...
│
├── phases/             # (Optioneel) Fase details
│   └── 01-feature/
│       ├── PLAN.md
│       └── SUMMARY.md
│
└── research/           # (Optioneel) Onderzoek
    └── topic.md
```

---

## GSD Commands (Belangrijkste)

### Dagelijks

```bash
/gsd:progress          # Start ELKE sessie hiermee
```

### Planning

```bash
/gsd:plan-phase [n]    # Maak plan voor fase N
/gsd:execute-plan      # Voer plan uit
/gsd:verify-work       # Test wat je gebouwd hebt
```

### Context

```bash
/gsd:pause-work        # Pauzeer met context bewaren
/gsd:resume-work       # Hervat met context herstel
/gsd:add-todo          # Snel iets vastleggen
```

### Setup (eenmalig)

```bash
/gsd:new-project       # Maak PROJECT.md
/gsd:create-roadmap    # Maak ROADMAP.md
/gsd:map-codebase      # Analyseer code (optioneel)
```

---

## Workflow

### Sprint/Todo Werkwijze (Dagelijks)

```
Sessie starten:
"Wat staat er op de todo?"
→ Claude toont TODO tabel uit STATE.md

Item oppakken:
"Ik wil werken aan TASK-042"
→ Claude leest details uit BACKLOG.md
→ Gaat aan de slag

Item afronden:
"TASK-042 is klaar"
→ Claude zet in Done sectie
→ Update BACKLOG.md status

Nieuw item:
"Voeg toe: nieuwe feature X"
→ Claude maakt TASK-xxx in BACKLOG.md
→ Voegt toe aan STATE.md
```

### GSD Workflow (Grote Features)

```
1. /gsd:progress              ← Start hier
2. /gsd:plan-phase [n]        ← Maak plan
3. /gsd:execute-plan          ← Voer uit
4. /gsd:verify-work           ← Test
5. /gsd:progress              ← Check volgende stap
```

### Onderbroken Worden

```
1. /gsd:pause-work            ← Bewaar context
2. ... later ...
3. /gsd:resume-work           ← Herstel context
```

---

## Commit Convention

```
[FEAT] nieuwe feature         → Added (CHANGELOG)
[FIX] bug fix                 → Fixed
[DOCS] documentatie           → Documentation
[REFACTOR] code opschonen     → Refactored
[CHORE] maintenance           → Changed
[WIP] work in progress        → Skip CHANGELOG
```

---

## STATE.md - De Sleutel

Dit is het belangrijkste bestand. Er zijn twee varianten:

### Variant A: Todo Lijst (Aanbevolen)

Template: `.claude/get-shit-done/templates/state-todo.md`

```markdown
# Project State - Todo Lijst

**Last Updated:** 2026-01-21
**Session:** Backlog structuur opgeschoond

## Current Status

| Aspect | Status |
|--------|--------|
| **Current Task** | TASK-042 |
| **Blockers** | None |

## 📋 TODO LIJST

| TASK | Feature | Priority | Status |
|------|---------|----------|--------|
| TASK-040 | Projectstructuur | 🟠 High | 🔄 In Progress |
| TASK-042 | Verkoopcontracten | 🟠 High | ⏳ Todo |

## ✅ RECENT DONE

| TASK | Feature | Done |
|------|---------|------|
| TASK-039 | Audit log | 2026-01-20 |

## 📦 BACKLOG

| TASK | Feature | Priority |
|------|---------|----------|
| TASK-045 | Windmill test | 🟡 Medium |

## Sessie Notities

### 2026-01-21
- TASK-040 gestart
- Nieuwe templates gemaakt
```

### Variant B: GSD Phase Tracking

Template: `.claude/get-shit-done/templates/state.md`

Voor grote projecten met phases/plans/waves.

**Regel:** Als je niet weet waar je bent → lees STATE.md

---

## BACKLOG.md - TASK Structuur

Template: `.claude/get-shit-done/templates/backlog.md`

```markdown
# Backlog

## Priority Levels

| Priority | Betekenis |
|----------|-----------|
| 🔴 Critical | Blokkeert werk, moet direct |
| 🟠 High | Belangrijk, binnenkort oppakken |
| 🟡 Medium | Normaal, als er tijd is |
| 🟢 Low | Nice to have |

## Backlog Items

### [TASK-042] Verkoopcontracten Fix
**Priority:** 🟠 High
**Status:** 📋 Todo
**Assignee:** backend-specialist
**Effort:** L (4-6 hours)

**User Story:** Als verkoper wil ik dat het afroepschema correct werkt,
zodat ik contracten kan beheren zonder workarounds.

**Acceptance Criteria:**
- [ ] Bug gereproduceerd
- [ ] Fix geïmplementeerd
- [ ] Henri heeft getest
```

### TASK Effort Schattingen

| Size | Uren | Typisch voor |
|------|------|--------------|
| S | 1-2 | Kleine bugfix |
| M | 2-4 | Feature toevoeging |
| L | 4-6 | Nieuwe module |
| XL | 6+ | Grote feature |

---

## Wanneer Welk Bestand?

| Situatie | Bestand |
|----------|---------|
| "Waar was ik gebleven?" | STATE.md |
| "Wat is de scope?" | PROJECT.md |
| "Welke fase nu?" | ROADMAP.md |
| "Wat staat open?" | BACKLOG.md |
| "Hoe werkt dit?" | README.md |

---

## Tips

1. **Start ALTIJD met `/gsd:progress`** - Het leest STATE.md en geeft je context
2. **Update STATE.md regelmatig** - Niet pas aan eind van sessie
3. **Gebruik BACKLOG.md voor alles** - Bugs, ideas, todos
4. **Commit messages = documentatie** - Gebruik de [TAG] convention

---

## Kopiëren naar Nieuw Project

```bash
# Automatisch (via script)
./deploy/scripts/new-project.sh [klant] [project]

# Handmatig
cp -r deploy/templates/project-skeleton/.planning/ [project]/.planning/
```

---

*Framework versie: 1.2 - 2026-01-22*

---

## Templates

Alle templates staan in `.claude/get-shit-done/templates/`:

| Template | Doel |
|----------|------|
| `state-todo.md` | STATE.md voor sprint/todo werkwijze |
| `state.md` | STATE.md voor volledige GSD (phases) |
| `backlog.md` | BACKLOG.md met TASK structuur |
| `changelog.md` | CHANGELOG.md met commit convention |
| `claude-md-todo-section.md` | **CLAUDE.md sectie** voor todo workflow |
| `project.md` | PROJECT.md basis |
| `roadmap.md` | ROADMAP.md met phases |

### CLAUDE.md Integratie

Voeg de todo workflow sectie toe aan je project CLAUDE.md zodat Claude bij elke sessie weet hoe de werkwijze werkt:

```markdown
## Todo / Backlog Workflow

**Bij elke sessiestart: check de todo lijst.**

"Wat staat er op de todo?" → Claude leest STATE.md

| Bestand | Doel |
|---------|------|
| STATE.md | Todo lijst (actieve items) |
| BACKLOG.md | Volledige TASK specs |
```

Zie `claude-md-todo-section.md` voor de volledige template.

---

## Git Workflow

### Bij TASK afronden:

```
1. Commit code:     git commit -m "[FEAT] TASK-042: beschrijving"
2. Update:          CHANGELOG.md, STATE.md, BACKLOG.md
3. Commit docs:     git commit -m "[DOCS] TASK-042 afgerond"
4. Push:            git push
```

### Commit Tags → CHANGELOG

| Tag | CHANGELOG Sectie |
|-----|------------------|
| [FEAT] | Added |
| [FIX] | Fixed |
| [DOCS] | Documentation |
| [REFACTOR] | Refactored |
| [CHORE] | Changed |
| [WIP] | — (skip) |

### Sync Commando

```
"Sync alles" of "Commit en push"
→ Claude commit alle wijzigingen
→ Update CHANGELOG.md
→ Push naar remote
```
