# Solution Workflow - Twee Patterns

> KRITISCH: Lees dit voordat je aan een solution werkt!

---

## Het Probleem

Solutions kunnen op twee manieren georganiseerd zijn:

```
Pattern A: Hub-Centric          Pattern B: Solution-Centric
─────────────────────────       ─────────────────────────────
solutions/agile-assistant/      solutions/RAG-automation/
├── (GEEN .git)                 ├── .git/  ← EIGEN REPO!
├── workflows/                  ├── .planning/
└── agents/                     └── workflows/

Git: Hub repo                   Git: Eigen repo
GSD: Hub's .planning/           GSD: Eigen .planning/
```

**BEIDE patterns zijn geldig.** Dit document legt uit wanneer welke.

---

## Pattern A: Hub-Centric (Tight Coupling)

### Kenmerken

- **Geen eigen .git** - Leeft in hub repo
- **GSD via hub** - `.planning/` van hub gebruiken
- **Commits gaan naar hub** - `git commit` in hub root

### Wanneer Gebruiken

- Solution is sterk gekoppeld aan hub
- Nog in development (niet stabiel genoeg voor eigen versioning)
- Interne tooling / experimenteel

### Voorbeeld: agile-assistant

```
VersnelDigitaal/                     ← HIER WERKEN
├── .git/                            ← Hub git
├── .planning/STATE.md               ← GSD tracking
└── solutions/
    └── agile-assistant/             ← GEEN eigen .git
        ├── workflows/
        ├── chat-ui/
        └── agents/
```

### Werkwijze

```bash
# 1. Start ALTIJD in hub root
cd C:\Users\ricks\VersnelDigitaal

# 2. Check status
/gsd:progress

# 3. Werk aan solution
# (edit files in solutions/agile-assistant/)

# 4. Commit vanuit hub root
git add .
git commit -m "[FEAT] agile-assistant: nieuwe chat feature"
git push

# 5. Update STATE.md in hub's .planning/
```

---

## Pattern B: Solution-Centric (Independent Product)

### Kenmerken

- **EIGEN .git** - Onafhankelijke repository
- **EIGEN .planning/** - Eigen GSD tracking
- **Kan apart gedeployed worden** - Standalone product
- **Agents blijven in hub** - Via parent inheritance

### Wanneer Gebruiken

- Solution is een **verkoopbaar product**
- Meerdere klanten gebruiken het (eigen versioning nodig)
- Stabiel genoeg voor release cycles
- Moet apart te clonen zijn door klanten

### Voorbeeld: RAG-automation

```
VersnelDigitaal/
├── .git/                            ← Hub git
├── .claude/agents/rag/              ← Agents HIER (niet in solution)
└── solutions/
    └── RAG-automation/
        ├── .git/                    ← EIGEN git!
        ├── .planning/               ← EIGEN planning
        │   ├── STATE.md
        │   └── PROJECT.md
        └── workflows/
```

### Werkwijze

```bash
# 1. Start in hub voor CONTEXT
cd C:\Users\ricks\VersnelDigitaal
/gsd:progress                        ← Hub status

# 2. Navigeer naar solution
cd solutions/RAG-automation

# 3. Check solution status (indien eigen .planning/)
cat .planning/STATE.md

# 4. Werk aan solution
# (edit files)

# 5. Commit in SOLUTION repo
git add .
git commit -m "[FEAT] nieuwe RAG pipeline"
git push                             ← Gaat naar RAG repo, NIET hub

# 6. Update solution's .planning/STATE.md
```

---

## KRITISCH: Waar Staan Agents?

**ALTIJD in de hub!**

```
VersnelDigitaal/
└── .claude/agents/
    ├── core/                ← Generieke agents
    ├── rag/                 ← RAG-specifieke agents
    ├── flow-mapper/         ← Flow-mapper agents
    └── agile/               ← Agile-assistant agents
```

**NOOIT:**
```
solutions/RAG-automation/.claude/agents/   ← FOUT!
```

**Waarom?**
- IP bescherming: Klant kloont solution, NIET de hub
- Parent inheritance: Claude leest agents van parent directory
- Centraal beheer: Alle agents op één plek

---

## Decision Tree: Welk Pattern?

```
Nieuwe solution maken?
│
├─▶ Is het een verkoopbaar product?
│   │
│   ├─▶ JA: Pattern B (eigen .git)
│   │   - Maak eigen repo
│   │   - Voeg .planning/ toe
│   │   - Agents blijven in hub
│   │
│   └─▶ NEE: Pattern A (hub git)
│       - Geen eigen .git
│       - Gebruik hub's .planning/
│       - Agents in hub
│
└─▶ Bij twijfel: Start met Pattern A
    Migreer later naar Pattern B als nodig
```

---

## Migratie: A → B

Als een solution volwassen wordt:

```bash
# 1. In solution folder
cd solutions/mijn-solution

# 2. Initialiseer eigen repo
git init
git add .
git commit -m "[INIT] eigen repository"

# 3. Maak .planning/
mkdir .planning
# Kopieer templates van hub

# 4. Push naar eigen repo
git remote add origin https://github.com/VersnelDigitaal/mijn-solution.git
git push -u origin master

# 5. Update hub's .gitignore
# Voeg solutions/mijn-solution/ toe
```

---

## Overzicht Huidige Solutions

| Solution | Pattern | Heeft .git | Heeft .planning | Status |
|----------|---------|------------|-----------------|--------|
| agile-assistant | A (Hub) | ❌ | ❌ (via hub) | Development |
| RAG-automation | B (Eigen) | ✅ | ❌ (TODO) | Product |
| Flow-mapper | B (Eigen) | ✅ | ❌ (TODO) | Planned |

---

## Checklist: Voor Je Begint

### Pattern A (Hub-Centric)

- [ ] Je bent in `C:\Users\ricks\VersnelDigitaal`
- [ ] Je hebt `/gsd:progress` gerund
- [ ] Je weet welke solution je gaat aanpassen
- [ ] Je commit VANUIT hub root

### Pattern B (Solution-Centric)

- [ ] Je bent gestart in hub voor context
- [ ] Je bent dan naar `solutions/[naam]` gegaan
- [ ] Je hebt solution's `.planning/STATE.md` gelezen (indien aanwezig)
- [ ] Je commit VANUIT solution folder
- [ ] Agents staan in hub's `.claude/agents/`

---

## FAQ

### "Waar commit ik?"

| Pattern | Waar commit je |
|---------|---------------|
| A (Hub) | `C:\Users\ricks\VersnelDigitaal` |
| B (Eigen) | `C:\Users\ricks\VersnelDigitaal\solutions\[naam]` |

### "Waar staat GSD planning?"

| Pattern | .planning/ locatie |
|---------|-------------------|
| A (Hub) | `VersnelDigitaal/.planning/` |
| B (Eigen) | `solutions/[naam]/.planning/` |

### "Waar staan agents?"

**ALTIJD:** `VersnelDigitaal/.claude/agents/`

Nooit in solution folder zelf.

### "Wat als ik per ongeluk in verkeerde folder commit?"

Pattern A in solution folder:
```bash
# Geen probleem - er is geen .git dus git zoekt naar parent
```

Pattern B in hub folder:
```bash
# Let op! Je commit dan solution changes in hub repo
# Check altijd: pwd en git status
```

---

## Samenvatting

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   ALTIJD STARTEN IN HUB                                     │
│   cd C:\Users\ricks\VersnelDigitaal                         │
│   /gsd:progress                                             │
│                                                             │
│   DAN:                                                      │
│   ├─▶ Pattern A: Blijf in hub, werk aan solutions/          │
│   │                                                         │
│   └─▶ Pattern B: cd solutions/[naam], werk daar             │
│                  commit in solution repo                    │
│                                                             │
│   AGENTS: Altijd in hub's .claude/agents/                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

*Versie 1.0 - 2026-01-18*
