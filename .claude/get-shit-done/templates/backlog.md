# Backlog Template

Template voor `.planning/BACKLOG.md` — gedetailleerde task specs met user stories.

---

## Wanneer gebruiken?

Samen met `state-todo.md` voor sprint-gebaseerd werken:
- STATE.md = overzicht (wat staat er open?)
- BACKLOG.md = details (wat houdt elke task in?)

---

## File Template

```markdown
# Backlog

**Last Updated:** [YYYY-MM-DD]

Alle taken in de wachtrij. Wanneer todo leeg raakt → samen bepalen wat naar todo gaat.

---

## Priority Levels

| Priority | Betekenis |
|----------|-----------|
| 🔴 Critical | Blokkeert werk, moet direct |
| 🟠 High | Belangrijk, binnenkort oppakken |
| 🟡 Medium | Normaal, als er tijd is |
| 🟢 Low | Nice to have |

---

## Backlog Items

### [TASK-001] Feature Naam Hier
**Priority:** 🟠 High
**Status:** 📋 Todo
**Assignee:** [task-manager / backend-specialist / frontend-specialist / etc.]
**Docs:** [Link naar relevante docs of "None"]
**Dependencies:** [TASK-xxx of "None"]
**Blocked by:** [Wat blokkeert dit? of "None"]
**Effort:** [S (1-2 hours) / M (2-4 hours) / L (4-6 hours) / XL (6+ hours)]

**User Story:** Als [rol] wil ik [wat], zodat [waarom].

**Description:**
[Korte beschrijving van het probleem of de feature]

**Impact:**
- [Wat gebeurt er als we dit NIET doen?]
- [Risico's of gevolgen]

**Fix Required:**
- [Stap 1]
- [Stap 2]
- [Stap 3]

**Acceptance Criteria:**
- [ ] [Criterium 1]
- [ ] [Criterium 2]
- [ ] [Criterium 3]

---

### [TASK-002] Nog Een Feature
**Priority:** 🟡 Medium
**Status:** 📋 Todo
...

---

## Done (Archive)

### ~~[TASK-000] Afgeronde Feature~~ ✅ DONE ([YYYY-MM-DD])

---

## Oude Items (Te Reviewen)

> Items die nog niet in TASK-xxx formaat staan. Moeten worden omgezet of verwijderd.

- [ ] [Oud item 1]
- [ ] [Oud item 2]
```

---

## TASK Structuur Uitleg

### Verplichte velden

| Veld | Beschrijving |
|------|--------------|
| **Priority** | 🔴🟠🟡🟢 - bepaalt urgentie |
| **Status** | 📋 Todo / 🔄 In Progress / ✅ Done / 🚫 Blocked |
| **User Story** | Als [rol] wil ik [wat], zodat [waarom] |
| **Acceptance Criteria** | Checkboxes - wanneer is het klaar? |

### Optionele velden

| Veld | Beschrijving |
|------|--------------|
| **Assignee** | Wie pakt dit op? (agent type of persoon) |
| **Docs** | Link naar specs, designs, of bestaande docs |
| **Dependencies** | Welke andere TASKs moeten eerst? |
| **Blocked by** | Externe blokkades (niet andere TASKs) |
| **Effort** | S/M/L/XL schatting |
| **Impact** | Wat als we dit NIET doen? |
| **Fix Required** | Concrete stappen |
| **Description** | Context en achtergrond |

---

## Effort Schattingen

| Size | Uren | Typisch voor |
|------|------|--------------|
| S | 1-2 | Kleine bugfix, config change |
| M | 2-4 | Feature toevoeging, refactor |
| L | 4-6 | Nieuwe module, complexe fix |
| XL | 6+ | Grote feature, architectuur change |

---

## Workflow

### Nieuw item toevoegen

1. Bepaal TASK nummer (hoogste + 1)
2. Vul template in met minimaal: Priority, Status, User Story, Acceptance Criteria
3. Voeg korte regel toe aan STATE.md (todo of backlog sectie)

### Item naar todo verplaatsen

1. Update STATUS in BACKLOG.md naar 🔄 In Progress
2. Verplaats regel in STATE.md van "BACKLOG" naar "TODO LIJST"

### Item afronden + Git Sync

1. ✅ Check alle Acceptance Criteria af
2. 📝 **Git commit:**
   ```bash
   git add .
   git commit -m "[TAG] TASK-xxx: korte beschrijving"
   ```
3. 📋 **Update CHANGELOG.md** met wijziging
4. 📊 **Update STATUS** naar ✅ Done in BACKLOG.md
5. 🔄 **Verplaats in STATE.md** naar "RECENT DONE" met datum
6. 💾 **Commit docs:**
   ```bash
   git add .planning/ CHANGELOG.md
   git commit -m "[DOCS] TASK-xxx afgerond"
   ```

### Commit Tags

| Tag | Wanneer | CHANGELOG Sectie |
|-----|---------|------------------|
| [FEAT] | Nieuwe feature | Added |
| [FIX] | Bug fix | Fixed |
| [DOCS] | Documentatie | Documentation |
| [REFACTOR] | Code opschonen | Refactored |
| [CHORE] | Maintenance | Changed |
| [WIP] | Work in progress | — (skip) |

### Sync commando

```
"Sync alles" of "Commit en push"
→ Claude commit alle wijzigingen
→ Update CHANGELOG.md
→ Push naar remote
```

---

## Assignee Types

Gebruik agent types voor automatische context:

| Assignee | Expertise |
|----------|-----------|
| `task-manager` | Planning, prioritering, overzicht |
| `backend-specialist` | API, database, server logic |
| `frontend-specialist` | React, UI, forms |
| `database-specialist` | Schema, DDL, queries |
| `code-reviewer` | Review, security audit |

Of gebruik persoonsnamen voor externe taken.
