# JetFlux SDK v2.2.0

A Claude Code development environment with structured workflows, specialized agents, and 18 slash commands. Built on [everything-claude-code](https://github.com/affaan-m/everything-claude-code) by affaan-m.

## Features

- **21 Specialized Agents** - 8 core + 13 enhanced agents for different task types
- **18 Slash Commands** - Streamlined development workflows
- **6-Phase Development Workflow** - Structured approach from planning to deployment
- **Learning Pipeline** - `/learn` → `/instinct` → `/evolve` for continuous improvement

## Quick Start

### 1. New Project
```
/sdk ../my-project   → gather settings → create structure → generate docs/plan.md → stop
```
No code is written. Review `docs/plan.md`, then run `/run` to implement phase by phase.

### 2. Running Commands
```
project-settings.md (context) + /design (command) → context-aware planning
```

## Slash Commands (18 total)

| Category | Commands |
|----------|----------|
| **Core** | `/design`, `/run`, `/tdd`, `/code-review`, `/build-fix` |
| **Quality** | `/verify`, `/checkpoint` |
| **Operations** | `/sdk`, `/deploy`, `/release` |
| **Learning** | `/learn`, `/instinct`, `/evolve` |
| **Documentation** | `/update-docs`, `/wordlist` |
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
│  /sdk            → Create structure + plan (no code yet)    │
│  /sdk --update   → Refresh SDK files in existing project    │
│  /sdk --pm       → Configure/change package manager         │
│  /wordlist       → Generate domain vocabulary reference     │
│  /design         → Create/update plan for a feature         │
│  /update-docs    → Document initial structure               │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 2: IMPLEMENTATION (repeat for each feature)          │
├─────────────────────────────────────────────────────────────┤
│  /run             → Execute plan (smart TDD integration)    │
│  /checkpoint      → Save progress after milestone           │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 3: TESTING & QUALITY                                 │
├─────────────────────────────────────────────────────────────┤
│  /tdd             → Run tests (unit, integration, E2E)      │
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
│  PHASE 5: DOCUMENTATION & LEARNING                          │
├─────────────────────────────────────────────────────────────┤
│  /update-docs     → Sync all docs (README, codemaps, API)   │
│  /learn           → Extract patterns from session           │
│  /instinct        → View/manage learned instincts           │
│  /evolve          → Cluster instincts into commands/agents  │
│  /create-command  → Create new custom slash commands        │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  PHASE 6: DEPLOYMENT & RELEASE                              │
├─────────────────────────────────────────────────────────────┤
│  /deploy          → Docker, K8s, Vercel, Railway, etc.      │
│  /verify          → Final validation                        │
│  /release         → Version bump, changelog, git tag        │
└─────────────────────────────────────────────────────────────┘
```

## Quick Reference by Situation

| When | Use |
|------|-----|
| Starting a new project | `/sdk` (structure + plan only, no code) |
| Implementing the plan | `/run` (phase by phase) |
| Updating SDK in existing project | `/sdk --update` (refreshes SDK files) |
| Adding a feature | `/design` → `/run` → `/tdd` → `/checkpoint` |
| Complex cross-cutting work | `/orchestrate` (coordinates multiple phases) |
| Build broken | `/build-fix` |
| Before committing | `/code-review` → `/verify` |
| After major changes | `/update-docs` |
| Need domain vocabulary | `/wordlist` or `/wordlist "domain name"` |
| Capturing learnings | `/learn` → `/instinct` → `/evolve` |
| Testing AI features | `/ai-eval` |
| Deploying | `/deploy` or `/deploy vercel` |
| Creating custom workflows | `/create-command` |

## Minimum Viable Workflow

For quick tasks:
```
/design → /run → /tdd → /verify
```

## Directory Structure

```
jetflux-sdk/
├── .claude/
│   ├── commands/         # 18 slash commands (/sdk, /design, /run, /tdd, etc.)
│   ├── agents/           # 21 agents (8 core + 13 enhanced)
│   ├── plans/            # Implementation plans (created by /design)
│   ├── mcp-configs/      # MCP server configurations
│   └── checkpoints.log   # Quick checkpoint index
├── docs/
│   └── checkpoints/      # Checkpoint files (created by /checkpoint)
├── CLAUDE.md             # Master directives
├── project-settings.md   # Project setup template
└── README.md
```

## Available Agents

### Core Agents (8)
| Agent | Purpose |
|-------|---------|
| planner | Feature implementation planning |
| architect | System design decisions |
| tdd-guide | TDD methodology (RED/GREEN/REFACTOR) |
| code-reviewer | Quality and security review |
| build-error-resolver | Build/TypeScript error fixing |
| e2e-runner | Playwright E2E testing |
| refactor-cleaner | Dead code elimination |
| doc-updater | Documentation synchronization |

### Enhanced Agents (13)
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
| | `--no-backup` | Skip backup prompt during updates |
| | `--pm <manager>` | Set package manager (pnpm/npm/yarn/bun/pip) |
| | `--pm detect` | Auto-detect from lockfiles |
| `/deploy` | *(auto-detect)* | Auto-detect best platform |
| | `docker` | Docker/Docker Compose |
| | `kubernetes` | Kubernetes manifests |
| | `vercel` | Vercel deployment |
| | `railway` | Railway deployment |
| | `fly` | Fly.io deployment |
| | `cloudflare` | Cloudflare Workers/Pages |
| | `--no-docs` | Skip automatic /update-docs after deploy |
| `/release` | *(interactive)* | Prompts for version type |
| | `patch` | Bump patch (1.0.0 → 1.0.1) |
| | `minor` | Bump minor (1.0.0 → 1.1.0) |
| | `major` | Bump major (1.0.0 → 2.0.0) |
| | `--dry-run` | Preview without executing |

### Core Development

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/design` | *(interactive)* | Creates plan, saves to .claude/plans/current.md |
| `/run` | *(none)* | Execute current plan with smart TDD |
| | `--force-tdd` | Force TDD even if plan says No |
| | `--no-tdd` | Skip TDD even if plan says Yes |
| | `--phase N` | Start from specific phase |
| | `--dry-run` | Preview without executing |
| | `--test-type <type>` | Override test types (unit/integration/e2e/all) |
| `/tdd` | *(none)* | Run all tests |
| | `unit` | Unit tests only |
| | `integration` | Integration tests (NO MOCKING) |
| | `e2e` | E2E tests with Playwright |
| | `coverage` | Analyze coverage gaps |
| | `--full` | All tests + coverage + no-stubs |
| | `--from-plan` | Run tests based on plan's Test Strategy |
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
| `/checkpoint` | `create <name>` | Create named checkpoint (local) |
| | `create <name> --push` | Create checkpoint and push to remote |
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

### Documentation & Learning

| Command | Arguments/Flags | Description |
|---------|-----------------|-------------|
| `/update-docs` | *(auto)* | Sync all documentation |
| | `--readme` | Update README only |
| | `--codemaps` | Update codemaps only |
| | `--api` | Update API docs only |
| | `--all` | Full documentation suite |
| | `preview` | Show without writing |
| | `force` | Write without confirmation |
| `/wordlist` | *(auto-detect)* | Detect domain from project, generate vocab card |
| | `{domain}` | Generate vocabulary for specific domain |
| `/learn` | *(auto-detect)* | Extract patterns from session |
| `/instinct` | *(none)* | Show instinct status (default) |
| | `status` | Show all learned instincts |
| | `export` | Export instincts for sharing |
| | `import <file>` | Import instincts from file/URL |
| | `--domain <name>` | Filter by domain |
| | `--high-confidence` | Show only high-confidence instincts |
| `/evolve` | *(none)* | Analyze and suggest evolutions |
| | `--execute` | Create the evolved structures |
| | `--dry-run` | Preview without creating |
| | `--domain <name>` | Only evolve specific domain |
| | `--threshold <n>` | Min instincts to cluster (default: 3) |

</details>

## Documentation

- [CLAUDE.md](CLAUDE.md) - Master directives and all commands
- [project-settings.md](project-settings.md) - Project setup template
- [.claude/commands/](.claude/commands/) - All 18 slash command files

## Releases

See [GitHub Releases](https://github.com/Jettan17/jetflux-cc-sdk/releases) for full changelog.

| Version | Highlights |
|---------|------------|
| **v2.2.0** | "Commercial" renamed to "Public" across init; CLI/Developer Tooling added as product type; Supabase removed from base MCPs |
| **v2.1.0** | `/sdk` no longer scaffolds frameworks or installs deps — creates structure + `docs/plan.md` only |
| **v2.0.0** | Standalone SDK: 8 core agents transferred, ECC plugin dependency removed |
| **v1.6.0** | Contextual workflow hints (`## Next Steps Output`) added to all 18 slash commands |
| **v1.5.0** | New `/wordlist` command, all 18 commands in workflow, backfilled release notes |
| **v1.4.3** | Strict `/design` behavior rules |
| **v1.4.2** | `/sdk --update` respects target project structure |
| **v1.4.1** | Exclude raw instincts from git tracking |
| **v1.4.0** | Learning pipeline (`/learn` → `/instinct` → `/evolve`), intelligent test selection |
| **v1.3.0** | New `/release` command |
| **v1.2.0** | Encapsulated `/setup-pm` into `/sdk` command |
| **v1.1.0** | `/deploy` captures deployment URL, auto-runs `/update-docs --readme` |
| **v1.0.0** | Current architecture established (`project-settings.md`, session requirements) |
| **v0.x** | Pre-release development (initial SDK through workflow restructuring) |

## Credits

Built on [everything-claude-code](https://github.com/affaan-m/everything-claude-code) by [affaan-m](https://github.com/affaan-m). Core agents and base command patterns adapted from the ECC plugin.

## License

MIT
