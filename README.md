# Claude Code Skills

Personal skills for Claude Code CLI.

## Available Skills

### Custom Skills

| Skill | Description | Trigger |
|-------|-------------|---------|
| reflect | Analyze conversations and propose skill improvements | `/reflect [skill-name]` |
| frontend-design | Modern, accessible frontend code with consistent design | UI/component requests |
| api-design | Consistent REST APIs with proper status codes and docs | API/endpoint requests |

### n8n Skills (from [czlonkowski/n8n-skills](https://github.com/czlonkowski/n8n-skills))

| Skill | Description |
|-------|-------------|
| n8n-expression-syntax | Expression `{{ }}` patterns and variable access |
| n8n-mcp-tools-expert | MCP tool usage and parameters |
| n8n-workflow-patterns | 5 architectural patterns for automation |
| n8n-validation-expert | Error interpretation and troubleshooting |
| n8n-node-configuration | Operation-aware node setup |
| n8n-code-javascript | JavaScript in Code nodes |
| n8n-code-python | Python in Code nodes |

## Structure

```
skills/
├── reflect/
│   └── SKILL.md
├── frontend-design/
│   └── SKILL.md
├── api-design/
│   └── SKILL.md
├── n8n-expression-syntax/
│   └── SKILL.md + supporting docs
├── n8n-mcp-tools-expert/
│   └── SKILL.md + guides
├── n8n-workflow-patterns/
│   └── SKILL.md + pattern docs
├── n8n-validation-expert/
│   └── SKILL.md + error catalog
├── n8n-node-configuration/
│   └── SKILL.md + dependencies
├── n8n-code-javascript/
│   └── SKILL.md + patterns
├── n8n-code-python/
│   └── SKILL.md + patterns
└── README.md
```

## n8n Skills Prerequisites

For n8n skills to work with MCP tools, install:

```bash
npm install -g n8n-mcp
```

Configure in `.mcp.json` with your n8n instance details.

## Usage

Skills are automatically activated based on context. For example:
- Ask about n8n expressions → activates `n8n-expression-syntax`
- Ask to build a workflow → activates `n8n-workflow-patterns`
- Ask about UI components → activates `frontend-design`

## Credits

- n8n skills: [czlonkowski/n8n-skills](https://github.com/czlonkowski/n8n-skills)
