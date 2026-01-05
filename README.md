# Claude Code Skills

Personal skills for Claude Code CLI.

## Available Skills

| Skill | Description | Trigger |
|-------|-------------|---------|
| reflect | Analyze conversations and propose skill improvements | `/reflect [skill-name]` |

## Structure

```
skills/
├── reflect/
│   ├── SKILL.md          # Skill definition
│   └── OBSERVATIONS.md   # Saved observations (optional)
├── [other-skill]/
│   └── SKILL.md
└── README.md
```

## Usage

Skills are invoked using slash commands in Claude Code:

```
/reflect frontend-design
```

## Adding New Skills

1. Create a new directory: `skills/[skill-name]/`
2. Add `SKILL.md` with the skill definition
3. Commit and push to sync across machines
