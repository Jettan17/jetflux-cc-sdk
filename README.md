# JetFlux SDK

A Claude Code development environment using **everything-claude-code (ECC)** for structured development workflows.

## Features

- **13 Enhanced Agents** - Specialized agents for different task types
- **21 Slash Commands** - Quick access to development workflows
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
instructions.md (context) + /plan (command) → context-aware planning
```

## Slash Commands (21 total)

| Category | Commands |
|----------|----------|
| **Core** | `/tdd`, `/plan`, `/code-review`, `/e2e`, `/build-fix`, `/refactor-clean` |
| **Quality** | `/verify`, `/checkpoint`, `/test-coverage`, `/no-stubs`, `/real-testing` |
| **Operations** | `/init`, `/deploy`, `/setup-pm` |
| **Documentation** | `/update-docs`, `/update-codemaps`, `/update-readme`, `/learn` |
| **Advanced** | `/eval`, `/orchestrate`, `/create-command` |

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
│  /init            → Initialize new project OR update SDK    │
│  /setup-pm        → Configure/change package manager        │
│  /plan            → Design implementation approach          │
│  /update-codemaps → Document initial structure              │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 2: IMPLEMENTATION (repeat for each feature)          │
├─────────────────────────────────────────────────────────────┤
│  /tdd             → Write tests FIRST, then implement       │
│  /no-stubs        → Verify no placeholder content           │
│  /checkpoint      → Save progress after milestone           │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 3: TESTING & QUALITY                                 │
├─────────────────────────────────────────────────────────────┤
│  /e2e             → Generate end-to-end tests               │
│  /real-testing    → Verify tests use real services          │
│  /test-coverage   → Check coverage gaps                     │
│  /eval            → Test AI features (if applicable)        │
│  /verify          → Run full validation                     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 4: REVIEW & CLEANUP                                  │
├─────────────────────────────────────────────────────────────┤
│  /code-review     → Quality and security review             │
│  /refactor-clean  → Remove dead code                        │
│  /build-fix       → Fix any build errors                    │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 5: DOCUMENTATION                                     │
├─────────────────────────────────────────────────────────────┤
│  /update-docs     → Sync documentation with code            │
│  /update-codemaps → Update architecture diagrams            │
│  /learn           → Extract patterns from session           │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 6: DEPLOYMENT                                        │
├─────────────────────────────────────────────────────────────┤
│  /deploy          → Docker/Kubernetes setup                 │
│  /verify          → Final validation                        │
└─────────────────────────────────────────────────────────────┘
```

## Quick Reference by Situation

| When | Use |
|------|-----|
| Starting a new project | `/init` (full setup) |
| Updating SDK in existing project | `/init --update` (refreshes SDK files) |
| Adding a feature | `/plan` → `/tdd` → `/no-stubs` → `/checkpoint` |
| Complex cross-cutting work | `/orchestrate` (coordinates multiple phases) |
| Build broken | `/build-fix` |
| Before committing | `/code-review` → `/verify` |
| After major changes | `/update-codemaps` → `/update-docs` |
| Updating project README | `/update-readme` |
| Testing AI features | `/eval` |
| Cleaning up | `/refactor-clean` |
| Deploying | `/deploy` |
| Creating custom workflows | `/create-command` |

## Minimum Viable Workflow

For quick tasks:
```
/plan → /tdd → /verify → /code-review
```

## Directory Structure

```
jetflux-sdk/
├── .claude/
│   ├── commands/         # 21 slash commands (/init, /tdd, /plan, etc.)
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
| `/init` | `[path]` | Target directory (optional) |
| | `--update` | Force update mode (refresh SDK files) |
| | `--no-git` | Skip git initialization |
| | `--no-framework` | Skip framework scaffolding |
| | `--no-backup` | Skip backup prompt during updates |
| `/setup-pm` | `--detect` | Show current package manager |
| | `--global <pm>` | Set global preference |
| | `--project <pm>` | Set project preference |
| | `--list` | List available package managers |
| `/deploy` | *(auto-detects)* | Detects project type automatically |

### Core Development

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/tdd` | *(interactive)* | TDD workflow with RED-GREEN-REFACTOR |
| `/plan` | *(interactive)* | Generates plan, waits for confirmation |
| `/build-fix` | *(auto)* | Incrementally fixes build errors |
| `/refactor-clean` | *(auto)* | Dead code analysis and removal |
| `/code-review` | *(none)* | Review local uncommitted changes |
| | `[PR-URL]` | Review a GitHub pull request |
| | `fix <issue-url>` | Analyze and fix a GitHub issue |
| `/e2e` | *(interactive)* | Generate Playwright E2E tests |

### Quality

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/verify` | *(none)* | Full verification suite |
| | `quick` | Quick verification only |
| `/checkpoint` | `create <name>` | Create named checkpoint |
| | `verify <name>` | Compare against checkpoint |
| | `list` | Show all checkpoints |
| | `clear` | Remove old checkpoints (keeps 5) |
| `/test-coverage` | *(auto)* | Analyze and generate missing tests |
| `/no-stubs` | *(auto)* | Scan for placeholder content |
| `/real-testing` | *(auto)* | Verify NO MOCKING policy compliance |

### Advanced

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/eval` | `define <name>` | Create eval definition |
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
| `/update-docs` | *(auto)* | Sync from source-of-truth |
| `/update-codemaps` | *(auto)* | Update architecture documentation |
| `/update-readme` | *(none)* | Full README generation |
| | `preview` | Show without writing |
| | `section <name>` | Update specific section only |
| | `force` | Write without confirmation |
| `/learn` | *(auto-detect)* | Extract patterns from session |

</details>

## Documentation

- [CLAUDE.md](CLAUDE.md) - Master directives and all commands
- [instructions.md](instructions.md) - Project setup template
- [.claude/commands/](.claude/commands/) - All 21 slash command files

## License

MIT
