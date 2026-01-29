# State Template - Todo Variant

Template voor `.planning/STATE.md` — lichtgewicht todo-gebaseerde tracking.

---

## Wanneer gebruiken?

- **Onderhoud & bugfixes** — ad-hoc werk zonder grote planning
- **Sprint-gebaseerd werken** — wekelijkse/tweewekelijkse sprints
- **Na initiële roadmap** — wanneer je in onderhoudsmodus bent
- **Kleinere projecten** — waar GSD phases te zwaar zijn

Voor grote greenfield projecten of complexe features, gebruik de volledige GSD flow met `state.md`.

---

## File Template

```markdown
# Project State - Todo Lijst

**Last Updated:** [YYYY-MM-DD]
**Session:** [Korte beschrijving laatste sessie]

---

## Current Status

| Aspect | Status |
|--------|--------|
| **Current Task** | [Wat ben je nu aan het doen?] |
| **Blockers** | [None / beschrijving] |
| **Mode** | [YOLO / Interactive] |

---

## 📋 TODO LIJST

> Actieve items. Details in [BACKLOG.md](BACKLOG.md).

| TASK | Feature | Priority | Status |
|------|---------|----------|--------|
| TASK-001 | [Feature naam] | 🟠 High | 🔄 In Progress |
| TASK-002 | [Feature naam] | 🟠 High | ⏳ Todo |
| - | [Ad-hoc item zonder TASK] | 🟡 Medium | ⏳ Todo |

---

## ✅ RECENT DONE

| TASK | Feature | Done |
|------|---------|------|
| TASK-000 | [Feature naam] | [YYYY-MM-DD] |

---

## 📦 BACKLOG (wacht op prioritering)

> Volledige lijst met details: [BACKLOG.md](BACKLOG.md)

| TASK | Feature | Priority |
|------|---------|----------|
| TASK-003 | [Feature naam] | 🟡 Medium |
| TASK-004 | [Feature naam] | 🟢 Low |

---

## 🚀 Werkwijze

**Sessie starten:**
\`\`\`
"Wat staat er op de todo?"
→ Claude toont bovenstaande tabel
\`\`\`

**Item oppakken:**
\`\`\`
"Ik wil werken aan TASK-002"
→ Claude leest details uit BACKLOG.md
→ Gaat aan de slag
\`\`\`

**Item afronden + Commit:**
\`\`\`
"TASK-002 is klaar"
→ Claude commit met [TAG] TASK-002: beschrijving
→ Claude zet in Done sectie
→ Update BACKLOG.md status
→ Update CHANGELOG.md
\`\`\`

**Nieuw item toevoegen:**
\`\`\`
"Voeg toe: nieuwe feature X"
→ Claude maakt TASK-xxx in BACKLOG.md (volledige structuur)
→ Voegt korte regel toe aan todo of backlog sectie hier
\`\`\`

---

## 🔄 Git Workflow

**Commit bij afronden TASK:**
\`\`\`bash
git add .
git commit -m "[TAG] TASK-xxx: korte beschrijving"
\`\`\`

**Commit tags:**
| Tag | Wanneer | CHANGELOG |
|-----|---------|-----------|
| [FEAT] | Nieuwe feature | Added |
| [FIX] | Bug fix | Fixed |
| [DOCS] | Documentatie | Documentation |
| [REFACTOR] | Code opschonen | Refactored |
| [CHORE] | Maintenance | Changed |
| [WIP] | Work in progress | Skip |

**Na commit:**
1. Update CHANGELOG.md met wijziging
2. Update STATE.md (TASK naar Done)
3. Update BACKLOG.md status

**Sync (optioneel):**
\`\`\`
"Sync alles"
→ Claude commit alle .planning/ wijzigingen
→ Push naar remote
\`\`\`

---

## Sessie Notities

### [YYYY-MM-DD]
- [Wat is er gedaan]
- [Belangrijke beslissingen]
- [Volgende stappen]
```

---

## Status Icons

| Icon | Status | Betekenis |
|------|--------|-----------|
| ⏳ | Todo | Nog niet gestart |
| 🔄 | In Progress | Actief mee bezig |
| ✅ | Done | Afgerond |
| 🚫 | Blocked | Wacht op iets anders |

## Priority Icons

| Icon | Priority | Betekenis |
|------|----------|-----------|
| 🔴 | Critical | Blokkeert werk, moet direct |
| 🟠 | High | Belangrijk, binnenkort oppakken |
| 🟡 | Medium | Normaal, als er tijd is |
| 🟢 | Low | Nice to have |

---

## TASK Nummering

- Gebruik `TASK-XXX` formaat (3 cijfers)
- Nummering is project-specifiek
- Ad-hoc items zonder TASK-nummer: gebruik `-` in TASK kolom
- Details altijd in BACKLOG.md

---

## Verschil met GSD State

| Aspect | GSD State | Todo State |
|--------|-----------|------------|
| Focus | Phases/Plans/Waves | Todo lijst |
| Tracking | Progress bars, velocity | Simpele tabellen |
| Overhead | Hoog (gestructureerd) | Laag (flexibel) |
| Best voor | Grote features | Onderhoud/sprints |

Je kunt beide combineren:
- GSD voor grote milestones
- Todo voor dagelijks werk ertussenin
