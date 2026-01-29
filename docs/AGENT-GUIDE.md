# Agent Guide

> Hoe je agents gebruikt en toevoegt

---

## Wat zijn Agents?

Agents zijn gespecialiseerde AI assistenten met specifieke kennis en focus. Ze helpen bij:

- Specifieke taken (API design, code review)
- Domein expertise (database, frontend)
- Consistente kwaliteit

---

## Beschikbare Agents

### Core Agents (standaard)

| Agent | Gebruik |
|-------|---------|
| **api-architect** | REST API design, validation, security |
| **code-reviewer** | QA, security review, best practices |
| **task-manager** | Planning, prioritering, tracking |
| **docs-manager** | CHANGELOG, documentatie |

### Infra Agents (optioneel)

| Agent | Gebruik |
|-------|---------|
| **docker-specialist** | Containers, docker-compose |
| **n8n-specialist** | Workflow automation |

### GSD Agents (intern)

Automatisch gebruikt door GSD framework - niet handmatig aanroepen.

---

## Agent Gebruiken

### Expliciet Aanroepen

```
# In Claude:
"Gebruik de code-reviewer om de login endpoint te checken"
"Vraag api-architect om het API schema te reviewen"
```

### Automatisch

Agents worden vaak automatisch gekozen op basis van context.

---

## Agent Toevoegen

### 1. Bepaal Categorie

```
Is altijd nuttig? → core/
Is voor infra/deployment? → infra/
Is project-specifiek? → [project]/
```

### 2. Maak Agent File

```bash
# In juiste folder
touch .claude/agents/[categorie]/[naam].md
```

### 3. Gebruik Template

```markdown
---
name: [agent-naam]
description: [korte beschrijving]
tools: Read, Write, Edit, Bash, Grep, Glob
---

# [Agent Naam]

## Expertise
- Skill 1
- Skill 2
- Skill 3

## Wanneer Gebruiken
- Situatie 1
- Situatie 2

## Standaarden
[Technische richtlijnen]

## Output Format
[Hoe agent output geeft]
```

### 4. Update Registry

Voeg toe aan `.claude/agents/REGISTRY.md`

### 5. Update Collaboration

Voeg toe aan `.claude/agents/COLLABORATION.md`

---

## Agent Best Practices

### Design
- Houd focus smal (1 domein)
- Duidelijke expertise lijst
- Concrete output format
- Wanneer WEL en NIET gebruiken

### Naming
- `[domein]-specialist.md`
- Lowercase, hyphens
- Descriptief

### Content
- Geef concrete voorbeelden
- Definieer standaarden
- Include checklists waar nuttig

---

## Voorbeeld Agents

### Minimal Agent

```markdown
# Logger Specialist

## Expertise
- Logging best practices
- Log levels
- Structured logging

## Tools
- Read, Edit

## Wanneer Gebruiken
- Logging toevoegen
- Log format standardiseren
```

### Uitgebreide Agent

```markdown
---
name: database-specialist
description: Database schema design en queries
tools: Read, Write, Edit, Bash, Grep, Glob
---

# Database Specialist

## Expertise
- Schema design
- Query optimization
- Indexing strategies
- Migration management

## Wanneer Gebruiken
- Nieuwe tabellen ontwerpen
- Query performance issues
- Database migraties

## Standaarden
- Naming: snake_case
- Primary keys: id (serial)
- Timestamps: created_at, updated_at

## Checklists

### Nieuwe Tabel
- [ ] Primary key gedefinieerd
- [ ] Foreign keys correct
- [ ] Indexes voor queries
- [ ] Timestamps aanwezig

## Output Format
- SQL statements met comments
- Migratie files indien nodig
```

---

## Tips

### Wanneer Agent Maken
- Herhaaldelijke taak type
- Specifieke domein kennis nodig
- Consistentie belangrijk

### Wanneer GEEN Agent
- Eenmalige taak
- Algemene vraag
- Geen specifieke expertise nodig

---

## Troubleshooting

### Agent niet gevonden
- Check bestandsnaam (lowercase, .md)
- Check folder locatie
- Werk vanuit hub root

### Agent geeft verkeerde output
- Update agent file met betere instructies
- Voeg voorbeelden toe
- Maak output format specifieker

---

*Goede agents = Consistente kwaliteit*
