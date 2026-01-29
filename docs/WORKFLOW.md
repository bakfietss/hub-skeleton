# Daily Workflow Guide

> Hoe je dagelijks met de hub werkt

---

## Sessie Starten

### Stap 1: Altijd vanuit hub root

```bash
cd /path/to/hub
claude
```

**NIET** vanuit een subdirectory starten!

### Stap 2: Check status

```bash
# In Claude:
/gsd:progress

# Of handmatig:
cat .planning/STATE.md
```

### Stap 3: Kies wat te doen

GSD progress toont:
- Actieve fase
- Open taken
- Blokkerende items
- Aanbevolen volgende stap

---

## Werken aan Taken

### Met GSD Framework

```bash
# Nieuwe milestone starten
/gsd:new-milestone

# Fase plannen
/gsd:plan-phase

# Fase uitvoeren
/gsd:execute-phase

# Voortgang checken
/gsd:progress
```

### Handmatig

1. Open `.planning/STATE.md`
2. Kies een taak
3. Werk eraan
4. Update status in STATE.md
5. Commit wijzigingen

---

## Git Workflow

### Commit Format

```
[TYPE] Korte beschrijving

Types:
[FEAT]     → Nieuwe feature
[FIX]      → Bug fix
[DOCS]     → Documentatie
[REFACTOR] → Code cleanup
[CHORE]    → Maintenance
[WIP]      → Work in progress (skip changelog)
```

### Voorbeeld

```bash
git add .
git commit -m "[FEAT] User authentication toegevoegd"
```

---

## Agents Gebruiken

### Core Agents (altijd beschikbaar)

| Agent | Wanneer |
|-------|---------|
| `code-reviewer` | Voor deployment of na grote changes |
| `task-manager` | Planning en prioritering |
| `api-architect` | API design werk |
| `docs-manager` | CHANGELOG updates |

### Aanroepen

```
# In Claude:
"Gebruik de code-reviewer om de nieuwe endpoints te checken"
"Vraag task-manager wat de volgende taak moet zijn"
```

---

## Solutions Werken

### In welke solution werk je?

```bash
# Claude werkt vanuit hub root
# Specificeer welke solution:
"In solutions/my-project, voeg feature X toe"
```

### Nieuwe solution starten

Zie [SOLUTION-GUIDE.md](SOLUTION-GUIDE.md)

---

## Sessie Afsluiten

### 1. Update STATE.md

```markdown
## Huidige Status
- Waar ben je gebleven?
- Wat is de volgende stap?
```

### 2. Commit wijzigingen

```bash
git add .
git commit -m "[TYPE] Beschrijving van werk"
```

### 3. Push (optioneel)

```bash
git push
```

---

## Tips

### Productiviteit
- Begin elke sessie met `/gsd:progress`
- Werk aan één taak tegelijk
- Commit vaak met duidelijke berichten

### Problemen
- Agent niet gevonden? → Check of je vanuit root werkt
- GSD werkt niet? → Check `.claude/commands/gsd/`
- Verloren context? → Lees STATE.md

### Best Practices
- Houd STATE.md actueel
- Documenteer beslissingen
- Review code voor deployment

---

*Zie andere docs voor specifieke onderwerpen*
