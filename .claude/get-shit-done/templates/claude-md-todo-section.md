# CLAUDE.md - Todo/Backlog Sectie

Template sectie om toe te voegen aan project CLAUDE.md bestanden.

---

## Kopieer dit naar je CLAUDE.md

```markdown
## Todo / Backlog Workflow

**Bij elke sessiestart: check de todo lijst.**

\`\`\`bash
# Vraag van gebruiker:
"Wat staat er op de todo?"

# Claude antwoordt met STATE.md inhoud
→ Lees .planning/STATE.md
\`\`\`

### Structuur

| Bestand | Doel | Inhoud |
|---------|------|--------|
| `.planning/STATE.md` | **Todo lijst** | Korte tabel met actieve items |
| `.planning/BACKLOG.md` | **Volledige specs** | TASK-xxx met user stories, acceptance criteria |

### STATE.md = Todo (actief)

Bevat alleen items waar we mee bezig zijn of binnenkort aan beginnen:
- Korte tabel: TASK | Feature | Priority | Status
- Link naar BACKLOG.md voor details
- Sessie notities

### BACKLOG.md = Specs (volledig)

Elk item heeft de volgende structuur:

\`\`\`markdown
### [TASK-XXX] Titel
**Priority:** 🔴 Critical / 🟠 High / 🟡 Medium / 🟢 Low
**Status:** 📋 Todo / 🔄 In Progress / ✅ Done
**Assignee:** agent-type
**Docs:** Referenties
**Dependencies:** Andere taken
**Blocked by:** Blokkers
**Effort:** S (1-2h) / M (2-4h) / L (4-6h) / XL (6h+)

**User Story:** Als [rol] wil ik [actie] zodat [reden].

**Description:** Wat moet er gebeuren.

**Impact:** Wat is het probleem als we dit niet doen.

**Fix Required:** Concrete stappen.

**Acceptance Criteria:**
- [ ] Criterium 1
- [ ] Criterium 2
\`\`\`

### Workflow

1. **Item oppakken:** "Ik wil werken aan TASK-042" → Lees details uit BACKLOG.md
2. **Item afronden:** "TASK-042 is klaar" → Verplaats naar Done in STATE.md
3. **Nieuw item:** "Voeg toe: feature X" → Maak TASK-xxx in BACKLOG.md, voeg korte regel toe aan STATE.md
```

---

## Waarom in CLAUDE.md?

De CLAUDE.md wordt automatisch geladen bij elke sessie. Door de todo workflow hier te documenteren:

1. **Claude weet direct** hoe het project werkt
2. **Consistente werkwijze** over alle sessies
3. **Geen herhaling nodig** van instructies

---

## Plaatsing

Zet deze sectie **na** de project-specifieke setup instructies, **voor** de technische architectuur.

Typische CLAUDE.md structuur:
```
1. Project intro
2. First-Time Setup
3. **Todo / Backlog Workflow** ← HIER
4. Development Commands
5. Architecture Overview
6. Tech Stack
```
