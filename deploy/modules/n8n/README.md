# N8N Module

> Workflow automation agent + skills

## What's Included

- `n8n-specialist.md` - Agent voor workflow design
- 7 n8n skills voor gedetailleerde expertise
- MCP server configuratie

## Installation

### 1. Copy Agent

```bash
cp deploy/modules/n8n/n8n-specialist.md .claude/agents/infra/
```

### 2. Copy Skills (Optional)

```bash
cp -r deploy/modules/n8n/skills/* .claude/skills/
```

### 3. Configure MCP Server

Add to `.mcp.json`:

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "N8N_API_URL": "https://your-n8n-instance.com",
        "N8N_API_KEY": "your-api-key"
      }
    }
  }
}
```

### 4. Update Registry

Add to `.claude/agents/REGISTRY.md`:

```markdown
### infra/ - Infrastructure & Deployment

| Agent | Doel | Toegevoegd |
|-------|------|------------|
| n8n-specialist | Workflow automation | [datum] |
```

## Usage

```
# In Claude:
"Gebruik n8n-specialist om een workflow te ontwerpen"
"Help me met een webhook workflow"
```

## Skills Available

| Skill | Purpose |
|-------|---------|
| n8n-expression-syntax | {{}} expression patterns |
| n8n-mcp-tools-expert | MCP tools guide |
| n8n-workflow-patterns | Architecture patterns |
| n8n-validation-expert | Error handling |
| n8n-node-configuration | Node setup |
| n8n-code-javascript | Code node JS |
| n8n-code-python | Code node Python |
