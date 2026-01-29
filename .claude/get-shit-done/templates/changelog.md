# Changelog Template

Template voor `CHANGELOG.md` — automatisch bijgewerkt bij elke TASK completion.

---

## Wanneer updaten?

- **Bij elke [FEAT], [FIX], [DOCS], [REFACTOR], [CHORE] commit**
- **NIET bij [WIP] commits** — die skippen CHANGELOG

---

## File Template

```markdown
# [Project Naam] - Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [YYYY-MM-DD]

### Added
- **[Feature naam]** - Korte beschrijving (TASK-xxx)
  - Detail 1
  - Detail 2

### Fixed
- **[Bug naam]** - Wat was het probleem, wat is de fix (TASK-xxx)

### Changed
- **[Wijziging]** - Wat is er veranderd (TASK-xxx)

### Documentation
- **[Doc naam]** - Wat is toegevoegd/gewijzigd

### Refactored
- **[Component]** - Wat is opgeschoond

---

## [YYYY-MM-DD]

### Added
...
```

---

## Sectie Mapping

| Commit Tag | CHANGELOG Sectie |
|------------|------------------|
| [FEAT] | Added |
| [FIX] | Fixed |
| [DOCS] | Documentation |
| [REFACTOR] | Refactored |
| [CHORE] | Changed |
| [WIP] | — (skip) |

---

## Format Guidelines

### Goed voorbeeld

```markdown
### Added
- **Transformer Scripts Module** - Centrale beheer van converter scripts in database (TASK-012)
  - TRANSFORMER_SCRIPTS tabel met versioning
  - Backend CRUD API
  - Frontend service + MyTransformers page
  - Public API endpoint voor Windmill
```

### Slecht voorbeeld

```markdown
### Added
- transformer scripts toegevoegd
```

---

## Workflow

### Bij TASK afronden:

1. **Commit code** met [TAG] prefix
2. **Update CHANGELOG.md**:
   - Voeg entry toe onder juiste datum
   - Gebruik juiste sectie (Added/Fixed/etc)
   - Refereer TASK-xxx
   - Voeg relevante details toe
3. **Commit CHANGELOG** (mag in zelfde commit of apart)

### Voorbeeld commit message:

```
[FEAT] TASK-012: Transformer Scripts module toegevoegd

- Database tabel met versioning
- CRUD API endpoints
- Frontend beheer pagina
```

---

## Datum Groepering

- Groepeer alle wijzigingen van dezelfde dag onder één datum header
- Nieuwste bovenaan
- Bij meerdere wijzigingen op één dag: combineer onder secties

```markdown
## [2026-01-21]

### Added
- Feature A (TASK-040)
- Feature B (TASK-041)

### Fixed
- Bug X (TASK-042)
```

---

## TASK Referenties

Altijd TASK-xxx refereren zodat:
- Traceerbaar naar BACKLOG.md
- Traceerbaar naar Jira (indien gekoppeld)
- Context behouden

```markdown
- **API Key Reason Dialogs** - Reason veld toegevoegd (TASK-015)
```
