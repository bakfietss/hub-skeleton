# PROJECT RULES - Klantgericht Werken

> VERPLICHTE regels voor werken in deze repository

## 1. Werklocatie

**ALTIJD werken vanuit root: `Klantgerichtwerken/`**

```bash
# GOED
cd C:\Users\ricks\Klantgerichtwerken
claude

# FOUT
cd C:\Users\ricks\Klantgerichtwerken\projects\klant-a
claude  # ← Ziet centrale .claude/ NIET
```

## 2. Klant Files Bewerken

Bewerk klant files via pad, niet door cd:

```bash
# GOED - vanuit root
Edit: klanten/klant-a/src/workflow.json

# FOUT - in klant folder
cd klanten/klant-a
Edit: src/workflow.json  # ← Verliest centrale tools
```

## 3. Klant Git Operaties

Via bash commando's:

```bash
# Pull klant changes
cd klanten/klant-a && git pull && cd ../..

# Commit naar klant repo
cd klanten/klant-a && git add . && git commit -m "[TYPE] message" && git push && cd ../..
```

## 4. Commit Format

### Centrale Repo (Klantgerichtwerken)

```
[TYPE] Korte beschrijving

Details indien nodig.

Klant: [naam] of "Centraal"
```

### Klant Repo

Volg klant's eigen conventie, of:
```
[TYPE] Korte beschrijving
```

**Types:**
- `[FEAT]` - Feature
- `[FIX]` - Bug fix
- `[DOCS]` - Documentatie
- `[DEPLOY]` - Deployment
- `[CONFIG]` - Configuratie
- `[CHORE]` - Onderhoud

## 5. Na Wijzigingen

### Centrale wijzigingen:
1. Update `.planning/CHANGELOG.md`
2. Update `.planning/STATE.md` indien nodig
3. Commit naar centrale repo

### Klant wijzigingen:
1. Commit naar klant repo (via bash)
2. Update `.planning/STATE.md` (actieve klanten sectie)

## 6. Nieuwe Solution Aanmaken

**VERPLICHTE structuur voor ELKE solution in `solutions/`:**

```
solutions/[naam]/
├── .planning/              ← VERPLICHT - NOOIT OVERSLAAN
│   ├── PROJECT.md          ← Vision, problem, solution
│   ├── STATE.md            ← Todo lijst, huidige status
│   ├── BACKLOG.md          ← Gedetailleerde TASK specs
│   └── ROADMAP.md          ← Fase planning
├── agents/                 ← VERPLICHT
│   └── README.md           ← Welke agents, configuratie
├── CLAUDE.md               ← Entry point voor Claude
└── README.md               ← Project overview
```

**Checklist (verplicht):**
- [ ] `.planning/PROJECT.md` aangemaakt
- [ ] `.planning/STATE.md` aangemaakt (kopieer format van bestaande solution)
- [ ] `.planning/BACKLOG.md` aangemaakt
- [ ] `.planning/ROADMAP.md` aangemaakt
- [ ] `agents/README.md` aangemaakt (welke agents, hoe geconfigureerd)
- [ ] `CLAUDE.md` aangemaakt
- [ ] `README.md` aangemaakt

**NOOIT een solution starten zonder volledige structuur.**

Dit geldt ook voor "quick wins" of kleine projecten.

**TIP:** Check ALTIJD een bestaande solution (bijv. `agile-assistant/`) voor het juiste patroon voordat je begint.

---

## 7. Nieuwe Klant Onboarden

```bash
# 1. Clone klant repo
cd projects
git clone [klant-repo-url] klant-naam
cd ..

# 2. Update STATE.md - voeg klant toe aan tabel

# 3. Maak klant folder structure indien nodig
mkdir -p klanten/klant-naam/n8n-workflows
```

## 8. Tools Updaten

```bash
# Check voor updates
bash tools/check-updates.sh

# Update specifieke tool
cd tools/n8n-mcp && git pull && npm run build && cd ../..
cd tools/get-shit-done && git pull && node bin/install.js --local && cd ../..
cd tools/n8n-skills && git pull && cp -r skills/* ../.claude/skills/ && cd ../..
```

## 9. Verboden

- ❌ Werken vanuit klanten/klant-x/ folder
- ❌ Klant credentials in centrale repo
- ❌ Productie data in git
- ❌ Commits zonder CHANGELOG update (voor significante changes)
- ❌ Direct pushen naar klant main zonder review (tenzij afgesproken)
- ❌ **Solution aanmaken zonder .planning/ structuur**
