# Hub Documentation Index

> Centrale documentatie voor deze hub

---

## Quick Start

```bash
# Elke sessie starten met:
/gsd:progress

# Of handmatig:
cat .planning/STATE.md
```

---

## Documentatie Overzicht

| Document | Doel |
|----------|------|
| [INSTALLATION.md](INSTALLATION.md) | Hub installatie & setup |
| [WORKFLOW.md](WORKFLOW.md) | Dagelijkse workflow |
| [SOLUTION-GUIDE.md](SOLUTION-GUIDE.md) | Nieuwe solution aanmaken |
| [AGENT-GUIDE.md](AGENT-GUIDE.md) | Agents gebruiken & toevoegen |
| [GSD-GUIDE.md](GSD-GUIDE.md) | Get Shit Done framework |

---

## Dagelijkse Bestanden

| Bestand | Doel | Update Frequentie |
|---------|------|-------------------|
| `.planning/STATE.md` | Huidige status, todo's | Elke sessie |
| `.planning/BACKLOG.md` | Open items, ideeën | Wekelijks |
| `.planning/ROADMAP.md` | Milestones, fases | Maandelijks |
| `CHANGELOG.md` | Alle wijzigingen | Per commit |

---

## Hub Structuur

```
hub/
├── .claude/                 ← Agents, GSD framework, skills
│   ├── agents/              ← Agent definities
│   ├── commands/gsd/        ← GSD commando's
│   └── get-shit-done/       ← GSD framework
│
├── .planning/               ← Hub-level planning
│   ├── STATE.md             ← ⭐ START HIER
│   ├── BACKLOG.md
│   ├── ROADMAP.md
│   └── PROJECT.md
│
├── docs/                    ← Documentatie
├── deploy/                  ← Templates & scripts
├── solutions/               ← Product development
├── klanten/                 ← Klant projecten
└── personal/                ← Experimenten
```

---

## Belangrijke Regels

### 1. Altijd vanuit hub root werken
```bash
# GOED
cd /path/to/hub
claude

# FOUT - Geen toegang tot agents
cd /path/to/hub/solutions/myproject
claude
```

### 2. Elke solution heeft volledige structuur
Zie [SOLUTION-GUIDE.md](SOLUTION-GUIDE.md)

### 3. GSD voor project management
Zie [GSD-GUIDE.md](GSD-GUIDE.md)

---

*Zie INSTALLATION.md voor eerste setup*
