# Agent Registry

> Centrale index van alle agents met categorisatie criteria

## Decision Tree: Waar hoort een agent?

```
Is de agent ALTIJD nuttig, ongeacht project?
├─ JA → core/
│   Voorbeelden: code-reviewer, task-manager, docs-manager
│
└─ NEE → Is het voor DEPLOYMENT/INFRASTRUCTURE?
    ├─ JA → infra/
    │   Voorbeelden: docker-specialist, n8n-specialist
    │
    └─ NEE → Is het voor een SPECIFIEK PROJECT?
        ├─ JA → [project-naam]/
        │   Voorbeelden: myproject/database-specialist
        │
        └─ NEE → Maak nieuwe categorie of heroverweeg
```

## Categorisatie Criteria

### core/ - Universele Agents
**Criteria:**
- Bruikbaar in ELK project
- Geen project-specifieke kennis nodig
- Algemene development practices

**Standaard agents:**
| Agent | Doel |
|-------|------|
| api-architect | REST API design, validation, security |
| code-reviewer | QA, security, OWASP, best practices |
| task-manager | Planning, prioritering, tracking |
| docs-manager | CHANGELOG, documentatie |

---

### infra/ - Infrastructure & Deployment
**Criteria:**
- Gerelateerd aan deployment, hosting, automation
- Niet gebonden aan één project
- Herbruikbaar voor meerdere projecten

**Beschikbaar via install (optioneel):**
| Agent | Doel |
|-------|------|
| docker-specialist | Containers, compose |
| n8n-specialist | Workflow automation |

---

### [project]/ - Project-Specifieke Agents
**Criteria:**
- Alleen relevant voor specifiek project/solution
- Specifieke tech stack kennis

**Voorbeelden:**
- `myproject/database-specialist`
- `myproject/frontend-specialist`

---

### gsd/ - GSD Interne Agents
**Criteria:**
- Automatisch door GSD framework
- NIET handmatig aanpassen

---

## Nieuwe Agent Toevoegen

### Checklist

- [ ] **Categorie bepaald** via decision tree
- [ ] **Agent bestand gemaakt** in juiste folder
- [ ] **REGISTRY.md bijgewerkt** (deze file)
- [ ] **COLLABORATION.md bijgewerkt** (wanneer gebruiken)

### Template

```markdown
# [Naam] Agent

## Expertise
- Punt 1
- Punt 2

## Tools
- Read, Write, Edit, Bash, Grep, Glob

## Wanneer Gebruiken
- Situatie 1
- Situatie 2

## Standaarden
[Tech stack, conventies]

## Output Format
[Hoe output te leveren]
```

---

## Uitbreiden

### Optionele Agent Packs (installeerbaar)

| Pack | Agents | Commando |
|------|--------|----------|
| n8n-workflow | n8n-specialist + skills | `/hub:install n8n` |
| docker | docker-specialist | `/hub:install docker` |
| rag | qdrant-specialist, rag-validator | `/hub:install rag` |
| [custom] | project-specifiek | Handmatig toevoegen |

Zie `docs/INSTALLATION.md` voor installatie instructies.

---

*Laatst bijgewerkt: [datum]*
