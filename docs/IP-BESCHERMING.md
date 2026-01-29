# IP Bescherming - Hoe Het Werkt

> Bescherming van je intellectual property (agents, prompts, orchestratie)

---

## Het Principe

```
JOUW HUB (Rick)                      KLANT REPO
────────────────────                 ────────────────────
VersnelDigitaal/                     C:\Klant\RAG-project\
├── .claude/                         ├── (GEEN .claude/)
│   └── agents/        ◄── IP       │
│       ├── rag/                     ├── workflows/
│       ├── agile/                   ├── config/
│       └── ...                      └── BUSINESS-RULES.md
│
├── solutions/
│   └── RAG-automation/   ── clone ──▶  Klant kloont dit
│       ├── workflows/
│       └── README.md
│
└── .planning/
```

**Klant krijgt NOOIT:**
- `.claude/agents/` (jouw prompts, orchestratie)
- Hub-level planning docs
- Andere solutions

**Klant krijgt WEL:**
- Solution code (workflows, docker, config)
- `BUSINESS-RULES.md` (wat zij mogen aanpassen)
- Basic `CLAUDE.md` (minimale instructies)

---

## Hoe Werkt Het Technisch?

### 1. Gescheiden Git Repos

```
Hub repo:        github.com/VersnelDigitaal/VersnelDigitaal
                 └── bevat .claude/agents/ (NIET publiek)

Solution repo:   github.com/VersnelDigitaal/RAG-automation
                 └── bevat GEEN .claude/ (publiek/klant)

Klant kloont:    solution repo, NIET hub
```

### 2. .gitignore Bescherming

**Hub's .gitignore:**
```
solutions/      # Solutions zijn separate repos
klanten/        # Klant data nooit in hub
```

**Solution's .gitignore:**
```
.env            # Credentials nooit committen
data/           # Runtime data
```

### 3. Parent Directory Inheritance (Claude Code)

Claude Code zoekt `.claude/` in parent directories:

```
Rick werkt in:     C:\VersnelDigitaal\solutions\RAG\
Claude zoekt:      C:\VersnelDigitaal\solutions\RAG\.claude\  ❌ niet gevonden
                   C:\VersnelDigitaal\solutions\.claude\      ❌ niet gevonden
                   C:\VersnelDigitaal\.claude\                ✅ GEVONDEN!

Klant werkt in:    C:\Klant\RAG-project\
Claude zoekt:      C:\Klant\RAG-project\.claude\              ❌ niet gevonden
                   C:\Klant\.claude\                          ❌ niet gevonden
                   C:\.claude\                                ❌ niet gevonden
                   → Geen agents beschikbaar
```

**Resultaat:**
- Rick: Ziet alle agents via parent inheritance
- Klant: Ziet geen agents (tenzij je ze expliciet toevoegt)

---

## Wat Is Beschermd?

| Item | Waar | Klant Ziet? |
|------|------|-------------|
| **Agent prompts** | `.claude/agents/` | ❌ Nee |
| **GSD commands** | `.claude/commands/` | ❌ Nee |
| **Orchestratie** | `.claude/get-shit-done/` | ❌ Nee |
| **Solution code** | `solutions/[naam]/` | ✅ Ja |
| **Business rules** | `BUSINESS-RULES.md` | ✅ Ja (mag aanpassen) |
| **Config templates** | `config/.env.example` | ✅ Ja |

---

## Scenario's

### Scenario A: Klant Kloont Solution

```bash
# Klant doet:
git clone https://github.com/VersnelDigitaal/RAG-automation.git
cd RAG-automation

# Klant krijgt:
├── workflows/
├── deploy/
├── docs/
├── BUSINESS-RULES.md
├── CLAUDE.md           ← Minimale versie
└── README.md

# Klant krijgt NIET:
├── .claude/agents/     ← Bestaat niet in solution repo
```

### Scenario B: Rick Werkt aan Solution

```bash
# Rick werkt vanuit hub:
cd C:\Users\ricks\VersnelDigitaal
cd solutions/RAG-automation

# Rick ziet:
# - Solution files (in solution folder)
# - PLUS: Agents via parent inheritance (uit hub's .claude/)
```

### Scenario C: Collega Overneemt

```bash
# Collega kloont HUB (niet solution):
git clone https://github.com/VersnelDigitaal/VersnelDigitaal.git
cd VersnelDigitaal

# Collega krijgt ALLES:
# - Alle agents
# - Alle solutions
# - Alle planning docs
```

---

## Validatie: Test Je Setup

### Test 1: Klant Perspectief Simuleren

```bash
# Maak temp folder (simuleert klant)
mkdir C:\temp\klant-test
cd C:\temp\klant-test

# Clone solution (niet hub)
git clone https://github.com/VersnelDigitaal/RAG-automation.git
cd RAG-automation

# Check: geen .claude/
ls -la .claude/
# → Moet "No such file or directory" geven

# Check: CLAUDE.md is minimal
cat CLAUDE.md
# → Moet NIET hub-specifieke info bevatten
```

### Test 2: Jouw Perspectief

```bash
cd C:\Users\ricks\VersnelDigitaal\solutions\RAG-automation

# Check: agents toegankelijk via parent
# In Claude Code:
# → Agents moeten werken

# Check: geen lokale .claude/
ls -la .claude/
# → Moet "No such file or directory" geven
```

---

## Wat Als Klant Agents Nodig Heeft?

**Optie A: Minimal agents meegeven**

Maak een `solution/.claude/agents/` met ALLEEN wat klant nodig heeft:
```
RAG-automation/
└── .claude/
    └── agents/
        └── rag-user-agent.md   ← Beperkte versie
```

**Optie B: Geen agents (recommended)**

Klant werkt zonder Claude Code. Ze gebruiken alleen:
- N8N workflows (UI)
- BUSINESS-RULES.md (text editor)

---

## Checklist: IP Bescherming

- [ ] Solution repo bevat GEEN `.claude/` folder
- [ ] Solution repo bevat GEEN link naar hub agents
- [ ] Hub's `.gitignore` bevat `solutions/`
- [ ] Klant kan NIET bij hub repo (private of apart account)
- [ ] BUSINESS-RULES.md bevat geen IP (alleen WAT, niet HOE)
- [ ] CLAUDE.md in solution is minimal

---

## Risico's

| Risico | Mitigatie |
|--------|-----------|
| Per ongeluk agents committen | Check voor push: `git status` |
| Klant ziet hub repo | Hou hub private of apart |
| Collega deelt verkeerd | Training + documentatie |
| BUSINESS-RULES bevat IP | Review voor levering |

---

## Samenvatting

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   IP BESCHERMING = GESCHEIDEN REPOS                         │
│                                                             │
│   Hub:      .claude/agents/ (jouw IP)                       │
│             ↓                                               │
│   Solution: Geen .claude/ (klant krijgt dit)                │
│                                                             │
│   Rick:     Werkt vanuit hub → ziet agents                  │
│   Klant:    Werkt standalone → ziet GEEN agents             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

*Versie 1.0 - 2026-01-18*
