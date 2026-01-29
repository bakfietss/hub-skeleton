# Docker Module

> Container management agent

## What's Included

- `docker-specialist.md` - Agent voor container management
- Docker compose templates

## Installation

### 1. Copy Agent

```bash
cp deploy/modules/docker/docker-specialist.md .claude/agents/infra/
```

### 2. Update Registry

Add to `.claude/agents/REGISTRY.md`:

```markdown
### infra/ - Infrastructure & Deployment

| Agent | Doel | Toegevoegd |
|-------|------|------------|
| docker-specialist | Containers, compose | [datum] |
```

## Usage

```
# In Claude:
"Gebruik docker-specialist om een compose file te maken"
"Help me met container deployment"
```

## Key Concepts

### Infrastructure vs Solutions

```
INFRASTRUCTURE (centraal, eenmalig)
├── Caddy (reverse proxy)
├── N8N (workflow platform)
└── Maakt "proxy" network

SOLUTIONS (per project)
├── Project-specifieke services
└── Connecten naar "proxy" network
```

### Deployment Flow

1. Deploy infrastructure first
2. Deploy solutions (connect to proxy network)
3. Configure N8N with solution URLs
4. Import workflow JSONs
