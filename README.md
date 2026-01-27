# JetFlux SDK

A Claude Code development environment using **everything-claude-code (ECC)** for structured development workflows.

## Features

- **13 Enhanced Agents** - Specialized agents for different task types
- **14 Slash Commands** - Streamlined development workflows
- **6-Phase Development Workflow** - Structured approach from planning to deployment

## Quick Start

### 1. Install Plugin (if not installed)
```bash
/plugin marketplace add affaan-m/everything-claude-code
/plugin install everything-claude-code
/plugin list  # verify installation
```

### 2. Project Initialization
On first session, Claude prompts for project settings (scope, product type, objective). These are saved to `instructions.md`.

### 3. Running Commands
```
instructions.md (context) + /design (command) → context-aware planning
```

## Slash Commands (14 total)

| Category | Commands |
|----------|----------|
| **Core** | `/tdd`, `/design`, `/code-review`, `/build-fix` |
| **Quality** | `/verify`, `/checkpoint` |
| **Operations** | `/sdk`, `/deploy`, `/setup-pm` |
| **Documentation** | `/update-docs`, `/learn` |
| **Advanced** | `/ai-eval`, `/orchestrate`, `/create-command` |

## Complete Development Workflow

```
┌─────────────────────────────────────────────────────────────┐
│  PHASE 0: ORCHESTRATION (for complex tasks only)            │
├─────────────────────────────────────────────────────────────┤
│  /orchestrate  → Use when task touches 3+ areas or needs    │
│                  multiple agents working together           │
│                  Example: "Add authentication" (frontend,   │
│                  backend, database, tests all at once)      │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 1: SETUP & PLANNING                                  │
├─────────────────────────────────────────────────────────────┤
│  /sdk            → Initialize new project OR update SDK    │
│  /setup-pm        → Configure/change package manager        │
│  /design            → Design implementation approach          │
│  /update-docs     → Document initial structure              │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 2: IMPLEMENTATION (repeat for each feature)          │
├─────────────────────────────────────────────────────────────┤
│  /tdd             → Write tests FIRST, then implement       │
│  /tdd e2e         → End-to-end tests with Playwright        │
│  /checkpoint      → Save progress after milestone           │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 3: TESTING & QUALITY                                 │
├─────────────────────────────────────────────────────────────┤
│  /tdd --full      → Complete test suite + coverage          │
│  /ai-eval         → Test AI features (if applicable)        │
│  /verify          → Run full validation                     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 4: REVIEW & CLEANUP                                  │
├─────────────────────────────────────────────────────────────┤
│  /code-review     → Quality review + dead code cleanup      │
│  /build-fix       → Fix any build errors                    │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 5: DOCUMENTATION                                     │
├─────────────────────────────────────────────────────────────┤
│  /update-docs     → Sync all docs (README, codemaps, API)   │
│  /learn           → Extract patterns from session           │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 6: DEPLOYMENT                                        │
├─────────────────────────────────────────────────────────────┤
│  /deploy          → Docker, K8s, Vercel, Railway, etc.      │
│  /verify          → Final validation                        │
└─────────────────────────────────────────────────────────────┘
```

## Quick Reference by Situation

| When | Use |
|------|-----|
| Starting a new project | `/sdk` (full setup) |
| Updating SDK in existing project | `/sdk --update` (refreshes SDK files) |
| Adding a feature | `/design` → `/tdd` → `/checkpoint` |
| Complex cross-cutting work | `/orchestrate` (coordinates multiple phases) |
| Build broken | `/build-fix` |
| Before committing | `/code-review` → `/verify` |
| After major changes | `/update-docs` |
| Testing AI features | `/ai-eval` |
| Deploying | `/deploy` or `/deploy vercel` |
| Creating custom workflows | `/create-command` |

## Minimum Viable Workflow

For quick tasks:
```
/design → /tdd → /verify → /code-review
```

## Directory Structure

```
jetflux-sdk/
├── .claude/
│   ├── commands/         # 14 slash commands (/sdk, /tdd, /design, etc.)
│   ├── agents/           # 13 enhanced agents
│   └── mcp-configs/      # MCP server configurations
├── CLAUDE.md             # Master directives
├── instructions.md       # Project setup template
└── README.md
```

## Available Agents

### Core Agents
Planner, Architect, TDD Guide, Code Reviewer, Build Error Resolver, E2E Runner, Refactor Cleaner, Doc Updater

### Enhanced Agents (13 total)
| Agent | Purpose |
|-------|---------|
| ultrathink-analyst | Deep failure analysis |
| requirements-analyst | Requirements breakdown |
| framework-advisor | Tech stack decisions |
| intermediate-reviewer | Progress validation |
| todo-manager | Task management |
| gh-manager | GitHub Projects integration |
| deployment-specialist | Docker/K8s deployment |
| ui-engineer | UI/UX, React 19, Next.js 15, accessibility |
| flutter-specialist | Flutter mobile |
| security-auditor | OWASP Top 10, vulnerability scanning |
| deep-reflector | Session analysis, learning capture |
| gold-standards-validator | Code compliance enforcement |
| documentation-validator | Documentation accuracy checking |

## Command Reference

<details>
<summary>Click to expand full command reference with flags</summary>

### Operations

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/sdk` | `[path]` | Target directory (optional) |
| | `--update` | Force update mode (refresh SDK files) |
| | `--no-git` | Skip git initialization |
| | `--no-framework` | Skip framework scaffolding |
| | `--no-backup` | Skip backup prompt during updates |
| `/setup-pm` | `--detect` | Show current package manager |
| | `--global <pm>` | Set global preference |
| | `--project <pm>` | Set project preference |
| | `--list` | List available package managers |
| `/deploy` | *(auto-detect)* | Auto-detect best platform |
| | `docker` | Docker/Docker Compose |
| | `kubernetes` | Kubernetes manifests |
| | `vercel` | Vercel deployment |
| | `railway` | Railway deployment |
| | `fly` | Fly.io deployment |
| | `cloudflare` | Cloudflare Workers/Pages |

### Core Development

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/tdd` | *(interactive)* | Interactive TDD workflow |
| | `unit` | Focus on unit tests |
| | `integration` | Integration tests (NO MOCKING) |
| | `e2e` | E2E tests with Playwright |
| | `coverage` | Analyze + generate missing tests |
| | `--full` | All tests + coverage + no-stubs |
| `/design` | *(interactive)* | Generates plan, waits for confirmation |
| `/build-fix` | *(auto)* | Incrementally fixes build errors |
| `/code-review` | *(none)* | Review local changes + dead code cleanup |
| | `--no-clean` | Skip dead code cleanup |
| | `[PR-URL]` | Review a GitHub pull request |
| | `fix <issue-url>` | Analyze and fix a GitHub issue |

### Quality

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/verify` | *(none)* | Full verification suite |
| | `quick` | Build + types only |
| | `pre-commit` | Checks for commits |
| | `pre-pr` | Full + security scan |
| | `--e2e` | Include E2E tests |
| | `--full` | All checks including E2E |
| `/checkpoint` | `create <name>` | Create named checkpoint |
| | `verify <name>` | Compare against checkpoint |
| | `list` | Show all checkpoints |
| | `clear` | Remove old checkpoints (keeps 5) |

### Advanced

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/ai-eval` | `define <name>` | Create AI eval definition |
| | `check <name>` | Run evals for feature |
| | `report <name>` | Generate full eval report |
| | `list` | Show all eval definitions |
| | `clean` | Remove old logs (keeps 10) |
| `/orchestrate` | `feature <desc>` | Full feature workflow |
| | `bugfix <desc>` | Bug fix workflow |
| | `refactor <desc>` | Refactoring workflow |
| | `security <desc>` | Security review workflow |
| | `custom <agents> <desc>` | Custom agent sequence |
| `/create-command` | `[name]` | Interactive command wizard |

### Documentation

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/update-docs` | *(auto)* | Sync all documentation |
| | `--readme` | Update README only |
| | `--codemaps` | Update codemaps only |
| | `--api` | Update API docs only |
| | `--all` | Full documentation suite |
| | `preview` | Show without writing |
| | `force` | Write without confirmation |
| `/learn` | *(auto-detect)* | Extract patterns from session |

</details>

## Documentation

- [CLAUDE.md](CLAUDE.md) - Master directives and all commands
- [instructions.md](instructions.md) - Project setup template
- [.claude/commands/](.claude/commands/) - All 14 slash command files

## License

MIT
