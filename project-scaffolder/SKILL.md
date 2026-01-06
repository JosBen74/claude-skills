---
name: project-scaffolder
description: Set up new Claude Code projects with CLAUDE.md files, slash commands, subagents, and proper structure using best practices
auto_activation: true
activation_keywords: ["scaffold", "new project", "skapa projekt", "sätt upp", "initialize", "create project", "CLAUDE.md"]
integrates_with:
  - frontend-design    # För React/Vue/frontend-projekt
  - api-design         # För backend/API-projekt
  - n8n-workflow-patterns  # För automation-projekt
notes: |
  - Aktiveras automatiskt vid projektuppstart
  - Använder frontend-design skill för UI-komponenter och styling
  - Använder api-design skill för REST API-struktur
  - Använder n8n-workflow-patterns för automationsprojekt
---

# Project Scaffolder Skill

## When to Use This Skill

Use this skill when:
- User asks to "set up a new project" or "create a new project"
- User asks to "create a CLAUDE.md" or "generate CLAUDE.md"
- User asks to "initialize Claude Code" for a project
- User asks to "scaffold" a project or "create project structure"
- User wants to add Claude Code support to existing code
- User asks to create custom slash commands or subagents
- User wants to create a new skill definition

Do NOT use this skill for:
- General coding questions unrelated to project setup
- Running or testing existing projects
- Debugging code issues

## Skill Integration

**IMPORTANT**: When scaffolding projects, automatically apply relevant skills:

### Frontend Projects (React, Vue, Svelte, etc.)
- Apply **frontend-design** skill for:
  - Color palette (dark theme default)
  - Typography and spacing system
  - Component patterns (buttons, cards, forms)
  - Accessibility requirements (WCAG AA)
  - CSS custom properties structure

### Backend/API Projects (FastAPI, Express, Django, etc.)
- Apply **api-design** skill for:
  - Resource-oriented URL structure
  - HTTP methods and status codes
  - Response formats (data/error schemas)
  - Pagination and filtering patterns
  - OpenAPI documentation structure

### Automation Projects (n8n, workflow automation)
- Apply **n8n-workflow-patterns** skill for:
  - Webhook processing patterns
  - HTTP API integration patterns
  - Database operation patterns
  - AI agent workflow patterns
  - Scheduled task patterns

### Fullstack Projects
- Apply BOTH frontend-design AND api-design skills
- Ensure consistency between frontend and backend

## Prerequisites

Before using this skill, ensure:
- Write access to target directory
- For existing projects: ability to read config files (package.json, pyproject.toml, etc.)
- Project Scaffolder templates available at: `C:\Users\josef\OneDrive\Dokument\Project scaffolder`

## Core Instructions

### Step 1: Determine Project Type and Context

Analyze the target directory to understand what kind of project is being scaffolded:

```bash
# Check for Node.js/TypeScript
ls package.json 2>/dev/null && echo "Node.js project"

# Check for Python
ls pyproject.toml requirements.txt setup.py 2>/dev/null && echo "Python project"

# Check for Go
ls go.mod 2>/dev/null && echo "Go project"

# Check for Rust
ls Cargo.toml 2>/dev/null && echo "Rust project"
```

If no config files exist, ask the user what type of project they want to create.

**Based on project type, identify which skills to integrate:**
| Project Type | Skills to Apply |
|--------------|-----------------|
| React/Vue/Svelte | frontend-design |
| FastAPI/Express/Django | api-design |
| Fullstack (Next.js, etc.) | frontend-design + api-design |
| n8n automation | n8n-workflow-patterns |
| CLI tool | (none specific) |

### Step 2: Fetch Reference Documentation

Before generating any CLAUDE.md or configuration, fetch the latest best practices:

1. **Claude Code Best Practices**: https://www.anthropic.com/engineering/claude-code-best-practices
2. **Building Effective Agents**: https://www.anthropic.com/engineering/building-effective-agents
3. **Agent Skills Guide**: https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills

Use WebFetch to retrieve current recommendations from these URLs.

### Step 3: Gather Project Information

For **new projects**, ask the user:
1. Project name
2. Project description/purpose
3. Primary language/framework
4. Any special requirements or integrations

For **existing projects**, extract from:
- README.md (description and purpose)
- Package config files (dependencies, scripts)
- Existing folder structure
- Git history (if available)

### Step 4: Generate CLAUDE.md

Select and customize the appropriate template from:
- `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\claude-md\react-typescript.md`
- `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\claude-md\python-api.md`
- `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\claude-md\fullstack.md`
- `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\claude-md\minimal.md`

**IMPORTANT**: Follow the WHAT/WHY/HOW framework:
- **WHAT**: Tech stack, project structure, key files
- **WHY**: Purpose of the project, what each part does
- **HOW**: Commands to run, how to verify changes

Replace all `{{PLACEHOLDER}}` values with actual project information.

**Include skill-specific guidelines in CLAUDE.md:**

For frontend projects, add:
```markdown
## Design System
Follow frontend-design skill guidelines:
- Dark theme colors (--bg-primary: #000000, etc.)
- 8px spacing system
- Accessible components (WCAG AA)
```

For API projects, add:
```markdown
## API Conventions
Follow api-design skill guidelines:
- Resource-oriented URLs (/users, /orders)
- Proper HTTP status codes
- Standard error response format
```

### Step 5: Create Slash Commands (Optional)

If the user needs custom workflows, create `.claude/commands/` with:

**Essential command templates:**
- `review.md` - Code review workflow
- `test-and-commit.md` - Quality check and commit
- `fix-issue.md` - Bug fix workflow

Copy from `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\commands\` and customize.

### Step 6: Create Subagents (Optional)

If specialized tasks are needed, create `.claude/agents/` with:

**Common subagent templates:**
- `code-reviewer.md` - Automated code review
- `debugger.md` - Debugging assistance
- `researcher.md` - Research and investigation

Copy from `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\agents\` and customize.

### Step 7: Create Skills (Optional)

For domain-specific capabilities, create skills in `skills/` directory:

Use the template at `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\skills\SKILL.template.md`.

### Step 8: Verify Setup

1. Ensure CLAUDE.md is valid markdown
2. Check that referenced commands/paths exist
3. Verify any scripts are executable
4. Test slash commands are recognized
5. Run any verification commands listed in CLAUDE.md

### Step 9: Provide Next Steps

Tell the user:
1. How to use the generated configuration
2. How to customize further
3. Recommended MCP servers for their stack
4. How to add this to version control

## Reference Files

For additional context, see:
- Templates directory: `C:\Users\josef\OneDrive\Dokument\Project scaffolder\templates\`
- Best practices: `C:\Users\josef\OneDrive\Dokument\Project scaffolder\docs\best-practices.md`
- Skill guide: `C:\Users\josef\OneDrive\Dokument\Project scaffolder\docs\skill-guide.md`
- Subagent guide: `C:\Users\josef\OneDrive\Dokument\Project scaffolder\docs\subagent-guide.md`
- Agent patterns: `C:\Users\josef\OneDrive\Dokument\Project scaffolder\docs\agent-patterns.md`

## Examples

### Example 1: New React Project (with frontend-design integration)

**User request:** "Set up a new React TypeScript project called my-dashboard"

**Actions:**
1. Create `my-dashboard/` directory
2. Run `npm create vite@latest . -- --template react-ts`
3. Read React TypeScript template
4. **Apply frontend-design skill** - include design system in CLAUDE.md
5. Generate CLAUDE.md with:
   - Color variables from frontend-design
   - Component patterns reference
   - Accessibility checklist
6. Create `.claude/commands/` with review and test commands
7. Provide setup confirmation and next steps

**Expected Output:**
```
my-dashboard/
├── CLAUDE.md           # Includes frontend-design guidelines
├── .claude/
│   └── commands/
│       ├── review.md
│       └── test-and-commit.md
├── src/
│   └── styles/
│       └── variables.css  # Design system variables
├── package.json
└── ...
```

### Example 2: Add Claude Code to Existing FastAPI Project (with api-design integration)

**User request:** "Add Claude Code support to my FastAPI project"

**Actions:**
1. Read existing pyproject.toml and requirements.txt
2. Analyze project structure (understand routes, models, etc.)
3. Fetch latest Python/API best practices
4. **Apply api-design skill** - include API conventions in CLAUDE.md
5. Generate CLAUDE.md tailored to FastAPI with:
   - URL structure guidelines
   - Response format standards
   - Error handling patterns
6. Add relevant slash commands (test, lint, migrate)
7. Suggest MCP servers for Python development

### Example 3: n8n Automation Project (with n8n-workflow-patterns integration)

**User request:** "Set up a new n8n automation project"

**Actions:**
1. Create project directory
2. **Apply n8n-workflow-patterns skill**
3. Generate CLAUDE.md with:
   - Workflow pattern reference
   - Node configuration guidelines
   - Validation checklist
4. Create commands for workflow validation
5. Reference n8n MCP tools

### Example 4: Create Custom Skill

**User request:** "Create a skill for database migrations in my Django project"

**Actions:**
1. Read skill template
2. Customize for Django migrations
3. Include common migration commands
4. Add verification steps
5. Create in `skills/database-migration/SKILL.md`

## Verification

After setup is complete, verify:

1. **Read CLAUDE.md** - Ensure it's coherent, accurate, and follows best practices
2. **Check skill integration** - Verify relevant skill guidelines are included
3. **Check commands** - Verify slash commands are recognized by Claude Code
4. **Test a command** - Try running `/review` or similar
5. **Run verification** - Execute any verification commands listed in CLAUDE.md
6. **Validate structure** - Ensure all referenced paths and files exist

## Troubleshooting

### CLAUDE.md not loading or recognized

**Solution:**
- Check file is named exactly `CLAUDE.md` (case-sensitive)
- Ensure it's in the project root directory
- Verify it's valid markdown without syntax errors

### Slash commands not appearing

**Solution:**
- Ensure commands are in `.claude/commands/` directory
- Check file names end with `.md`
- Verify markdown frontmatter has proper format
- Restart Claude Code or reload the project

### Templates not found

**Solution:**
- Verify the Project Scaffolder directory path is correct
- Use Read tool to check template files exist
- Use absolute paths when referencing templates

---

## Notes

- **Progressive Disclosure**: Keep CLAUDE.md concise (under 200 lines). Use slash commands and skills for specialized workflows.
- **Never Send an LLM to Do a Linter's Job**: Reference linter configs, don't include style guidelines in CLAUDE.md.
- **Less Is More**: Only include universally-applicable instructions in CLAUDE.md.
- **Verification Commands**: Always include commands Claude can run to validate its work.
- **Fetch Latest Docs**: Always check Anthropic's engineering blog for current best practices before scaffolding.
- **Skill Integration**: Always check if frontend-design, api-design, or n8n-workflow-patterns skills apply to the project type.
