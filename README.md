# JetFlux SDK

A comprehensive Claude Code development environment combining the **everything-claude-code** plugin with enhanced agents and skills from the Kailash development system.

## Features

- **20 Specialized Agents** - 9 from everything-claude-code + 11 enhanced agents
- **10 Slash Commands** - Quick access to common workflows
- **120+ Skill Files** - Patterns, guides, and best practices
- **9 MCP Integrations** - AWS, GCP, Azure, Linear, Jira, GitHub, Supabase, Vercel, Railway
- **7-Phase Development Workflow** - Structured approach from analysis to deployment

## Quick Start

### 1. Install Plugin (if not installed)
```bash
/plugin marketplace add affaan-m/everything-claude-code
/plugin install everything-claude-code
/plugin list  # verify installation
```

### 2. Project Initialization
On first session, Claude automatically prompts for project settings (scope, product type, objective). These are saved to `instructions.md` and referenced in all subsequent commands.

### 3. Running Commands
Run slash commands like `/plan`, `/tdd`, `/code-review` yourself. Claude uses the project context from `instructions.md` when executing them.

```
instructions.md (context) + /plan (command) → context-aware planning
```

## Slash Commands

| Command | Description |
|---------|-------------|
| `/tdd` | Test-driven development |
| `/plan` | Implementation planning |
| `/e2e` | E2E test generation |
| `/code-review` | Quality review |
| `/build-fix` | Build error resolution |
| `/refactor-clean` | Dead code removal |
| `/learn` | Pattern extraction |
| `/checkpoint` | Save verification state |
| `/verify` | Run verification loop |
| `/setup-pm` | Package manager config |
| `/orchestrate` | Chain multiple agents |
| `/eval` | Define success criteria |

### When to Use Each Command

```
/plan ─────────► Start of feature (plan implementation)
    │
/tdd ──────────► During implementation (write tests + code)
    │
/checkpoint ───► At milestones (save progress)
    │
/verify ───────► Periodically (check build/types/tests)
    │
/code-review ──► Before commit/PR (quality check)
    │
/learn ────────► After solving tricky problems (save patterns)
```

**Key commands:**
- `/verify quick` - Fast build + type check
- `/verify pre-pr` - Full check before PR
- `/orchestrate feature "description"` - Chains: planner → tdd → reviewer → security
- `/checkpoint create "name"` - Git-based save point

## Directory Structure

```
jetflux-sdk/
├── .claude/
│   ├── agents/           # 11 enhanced agents
│   ├── skills/           # 8 skill categories (~120 files)
│   ├── guides/           # 3 specialized guides
│   ├── mcp-configs/      # 5 MCP server configurations
│   └── success-factors.md
├── CLAUDE.md             # Master directives
├── instructions.md       # Project setup template
├── docs/
│   ├── architecture/
│   └── decisions/
└── README.md
```

## Available Agents

### Base Agents (everything-claude-code)
- Planner, Architect, TDD Guide, Code Reviewer, Security Reviewer
- Build Error Resolver, E2E Runner, Refactor Cleaner, Doc Updater

### Enhanced Agents
- ultrathink-analyst, requirements-analyst, framework-advisor
- intermediate-reviewer, gold-standards-validator, documentation-validator
- todo-manager, gh-manager, deployment-specialist
- react-specialist, flutter-specialist

## MCP Integrations

### Included
- GitHub, Supabase, Vercel, Railway (from everything-claude-code)
- AWS, GCP, Azure, Linear, Jira (additional configs in `.claude/mcp-configs/`)

### Setup MCP Servers

1. Copy the desired config from `.claude/mcp-configs/`
2. Set required environment variables
3. Add to your project's `.claude/settings.json`

## Development Workflow

1. **Analysis** - Use ultrathink-analyst and requirements-analyst
2. **Planning** - Use todo-manager and gh-manager
3. **Implementation** - Use /tdd and framework specialists
4. **Testing** - Use testing-specialist and documentation-validator
5. **Deployment** - Use deployment-specialist
6. **Release** - Use /code-review and pre-commit validation
7. **Review** - Use intermediate-reviewer for final critique

## Documentation

- [CLAUDE.md](CLAUDE.md) - Complete master directives
- [instructions.md](instructions.md) - Project setup template
- [.claude/success-factors.md](.claude/success-factors.md) - Lessons learned

## License

MIT
