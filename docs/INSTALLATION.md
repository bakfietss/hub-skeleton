# Hub Installation Guide

> Stap-voor-stap handleiding voor het opzetten van een nieuwe hub

---

## Fase 1: Basis Installatie

### 1.1 Repository Clonen

```bash
# Clone de hub-skeleton
git clone https://github.com/[jouw-username]/hub-skeleton.git my-hub
cd my-hub

# Verwijder git history en start vers
rm -rf .git
git init
git add .
git commit -m "[FEAT] Initial hub setup from skeleton"
```

### 1.2 Configuratie Aanpassen

**CLAUDE.md** - Pas aan voor jouw hub:
```markdown
# [Jouw Hub Naam]

> [Beschrijving van wat deze hub doet]
```

**README.md** - Pas aan met jouw info

### 1.3 Planning Initialiseren

```bash
# Start Claude en initialiseer planning
claude

# In Claude:
/gsd:new-project
```

Dit creëert:
- `.planning/PROJECT.md` - Jouw hub visie
- `.planning/STATE.md` - Eerste taken
- `.planning/ROADMAP.md` - Fases

---

## Fase 2: Optionele Modules Installeren

De hub komt met core functionaliteit. Extra modules zijn beschikbaar in `deploy/modules/`.

### 2.1 N8N Workflow Module

**Wat krijg je:** n8n-specialist agent + workflow automation

```bash
# 1. Kopieer de agent
cp deploy/modules/n8n/n8n-specialist.md .claude/agents/infra/

# 2. Maak .mcp.json aan (vanuit example)
cp .mcp.json.example .mcp.json
# Edit .mcp.json met jouw n8n credentials
```

**MCP Server configureren:**
```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "N8N_API_URL": "https://jouw-n8n-instance.com",
        "N8N_API_KEY": "jouw-api-key"
      }
    }
  }
}
```

**Update REGISTRY.md** om de nieuwe agent te registreren.

Zie `deploy/modules/n8n/README.md` voor volledige instructies.

### 2.2 Docker Module

**Wat krijg je:** docker-specialist agent voor container management

```bash
cp deploy/modules/docker/docker-specialist.md .claude/agents/infra/
```

Zie `deploy/modules/docker/README.md` voor details.

### 2.3 Custom Modules Toevoegen

1. Maak folder in `deploy/modules/[naam]/`
2. Voeg README.md toe met installatie instructies
3. Voeg agent file(s) toe
4. Documenteer in main INSTALLATION.md

### 2.4 Custom MCP Servers

```json
{
  "mcpServers": {
    "custom-server": {
      "command": "node",
      "args": [".claude/mcp/custom/index.js"],
      "description": "Beschrijving van de server"
    }
  }
}
```

---

## Fase 3: Eerste Project Aanmaken

### 3.1 Solution Aanmaken

```bash
# In Claude:
# Maak nieuwe solution in solutions/
mkdir -p solutions/my-first-project/.planning
mkdir -p solutions/my-first-project/agents
```

Zie [SOLUTION-GUIDE.md](SOLUTION-GUIDE.md) voor volledige structuur.

### 3.2 Klant Project Aanmaken (optioneel)

```bash
mkdir -p klanten/klant-naam/.planning
# Gebruik deploy/templates/project-skeleton als basis
```

---

## Fase 4: Verificatie

### 4.1 Check Structuur

```bash
# Verify folders bestaan
ls -la .claude/agents/
ls -la .planning/
ls -la docs/
```

### 4.2 Test GSD

```bash
# In Claude:
/gsd:progress
# Moet STATE.md tonen zonder errors
```

### 4.3 Test Agents

```bash
# In Claude:
# Vraag om een agent te gebruiken
"Gebruik de code-reviewer om X te checken"
# Moet agent kunnen vinden en gebruiken
```

---

## Troubleshooting

### Agent niet gevonden
- Check of `.claude/agents/` correct is gestructureerd
- Zorg dat je vanuit hub root werkt

### GSD commando's werken niet
- Check of `.claude/commands/gsd/` alle commands bevat
- Check of `.claude/get-shit-done/` framework bevat

### MCP Server connecteert niet
- Check `.mcp.json` syntax
- Verify credentials correct zijn
- Herstart Claude Code

---

## Volgende Stappen

1. Lees [WORKFLOW.md](WORKFLOW.md) voor dagelijks gebruik
2. Lees [GSD-GUIDE.md](GSD-GUIDE.md) voor project management
3. Maak eerste solution via [SOLUTION-GUIDE.md](SOLUTION-GUIDE.md)

---

*Voor vragen: check de docs of vraag Claude*
