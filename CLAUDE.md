# Claude Code SDK - Master Directives

This project combines the **everything-claude-code** plugin with enhanced agents and skills from the Kailash development system.

---

## ⚠️ CRITICAL: Project Initialization Check

**At the start of EVERY session, you MUST:**

1. **Read `instructions.md`** to load project context
2. **Check if Project Settings are empty** (Scope, Final Product, Objective are blank)
3. **If empty, IMMEDIATELY prompt the user** for project settings before doing anything else:
   - Scope (Small/Medium/Large)
   - Final Product (Web/Mobile/Desktop/Open-Ended)
   - Commercial or Personal Use
   - Objective/Use-Case (required)
   - Data Sources (optional)
   - Visual Style (optional)
   - External Tool Integration (optional)
   - Existing Product Reference (optional)
4. **Update `instructions.md`** with their responses
5. **Always reference Project Settings and Must Do** when running commands or making decisions

**If Project Settings ARE filled**, acknowledge them and proceed with the user's request.

## Quick Start

### Plugin Status: INSTALLED ✓
The everything-claude-code plugin is installed at `~/.claude/plugins/everything-claude-code/`

### Available Slash Commands (15 total)
| Command | Description |
|---------|-------------|
| `/tdd` | Test-driven development workflow |
| `/plan` | Implementation planning |
| `/e2e` | E2E test generation |
| `/code-review` | Quality review |
| `/build-fix` | Build error resolution |
| `/refactor-clean` | Dead code removal |
| `/learn` | Pattern extraction mid-session |
| `/checkpoint` | Verification state saving |
| `/verify` | Verification loop execution |
| `/setup-pm` | Package manager configuration |
| `/eval` | Evaluation harness |
| `/orchestrate` | Multi-agent orchestration |
| `/test-coverage` | Test coverage analysis |
| `/update-codemaps` | Update code maps |
| `/update-docs` | Update documentation |

---

## Specialized Subagents

### From everything-claude-code (Base)
| Agent | Purpose |
|-------|---------|
| **Planner** | Feature implementation planning |
| **Architect** | System design decisions |
| **TDD Guide** | Test-driven development methodology |
| **Code Reviewer** | Quality and security assessment |
| **Security Reviewer** | Vulnerability analysis |
| **Build Error Resolver** | Construction failure fixing |
| **E2E Runner** | Playwright testing automation |
| **Refactor Cleaner** | Dead code elimination |
| **Doc Updater** | Documentation synchronization |

### Enhanced Agents (From Kailash)
| Agent | Purpose | When to Use |
|-------|---------|-------------|
| **ultrathink-analyst** | Deep failure analysis, complexity assessment | Complex features, systemic issues, risk analysis |
| **requirements-analyst** | Requirements breakdown, ADR creation | Systematic analysis, architecture decisions |
| **framework-advisor** | Technology selection guidance | Choosing frameworks, tech stack decisions |
| **intermediate-reviewer** | Checkpoint reviews, progress validation | Reviewing todos and implementation milestones |
| **gold-standards-validator** | Compliance checking | Code validation, catching violations early |
| **documentation-validator** | Documentation testing | Testing code examples, ensuring doc accuracy |
| **todo-manager** | Task management and tracking | Creating and managing development task lists |
| **gh-manager** | GitHub Projects integration | Syncing requirements with GitHub, managing sprints |
| **deployment-specialist** | Docker/Kubernetes deployment | Production deployments, environment management |
| **react-specialist** | React 19/Next.js 15 patterns | Frontend implementation, React Flow editors |
| **flutter-specialist** | Flutter mobile patterns | Cross-platform mobile/desktop apps |

---

## Development Workflow Phases

### Phase 1: Analysis
```
1. > Use the ultrathink-analyst subagent to analyze requirements for [feature]
2. > Use the requirements-analyst subagent to create breakdown and ADR
3. > Use the framework-advisor subagent to recommend technology choices
```

### Phase 2: Planning
```
1. > Use the todo-manager subagent to create task breakdown
2. > Use the gh-manager subagent to sync with GitHub Projects
3. > Use the intermediate-reviewer subagent to validate plan
```

### Phase 3: Implementation
```
For each component:
1. Use /tdd to write tests first
2. > Use pattern-expert or framework-specific specialist for implementation
3. > Use the gold-standards-validator subagent for compliance
4. > Use the intermediate-reviewer subagent for progress review
```

### Phase 4: Testing
```
1. > Use the testing-specialist subagent for 3-tier test coverage
2. > Use the documentation-validator subagent to test code examples
```

### Phase 5: Deployment
```
1. > Use the deployment-specialist subagent for Docker/Kubernetes setup
```

### Phase 6: Release
```
1. Run /code-review for final quality check
2. Use pre-commit validation
3. Create PR with proper documentation
```

### Phase 7: Final Review
```
1. > Use the intermediate-reviewer subagent for final critique
```

---

## Success Factors

### What Works Well
1. **Systematic Task Completion** - Finish each task completely before moving on
2. **Test-First Development** - Write tests before implementation
3. **Real Infrastructure Testing** - NO MOCKING policy for integration tests
4. **Evidence-Based Tracking** - Use file:line references for clear audit trails
5. **Comprehensive Documentation** - Document as you go, not at the end
6. **Subagent Specialization** - Use the right agent for each task type
7. **Design System Foundation** - Create design system BEFORE features

### Lessons Learned
1. **Documentation Early** - Write guides during/after implementation
2. **Pattern Consistency** - Follow same structure across examples
3. **Incremental Validation** - Verify tests pass immediately
4. **Deprecation Fixes** - Address all deprecations immediately
5. **Responsive Testing** - Test at all breakpoints for every feature

---

## Critical Rules

### Code Quality
- Always prefer editing existing files over creating new ones
- Avoid over-engineering - only make directly requested changes
- Don't add features, refactor code, or make "improvements" beyond what was asked
- Remove unused code completely - no backward-compatibility hacks

### No Stubs or Placeholders (CRITICAL)
**NEVER leave incomplete or placeholder content in any deliverable:**

#### Forbidden in UI/Frontend:
- ❌ Lorem ipsum or any placeholder text
- ❌ "Coming soon", "Under construction", "TBD", "TODO" visible to users
- ❌ Empty pages, blank sections, or stub components
- ❌ Placeholder images (gray boxes, "image here" text)
- ❌ Non-functional buttons, links, or form elements
- ❌ Hardcoded sample data that should be dynamic

#### Forbidden in Code:
- ❌ `pass` statements in Python without implementation
- ❌ `// TODO: implement` comments left in production code
- ❌ Empty function bodies or stub methods
- ❌ `throw new Error("Not implemented")` patterns
- ❌ Commented-out code blocks meant for "later"

#### The Rule:
**If a feature isn't ready, don't include it at all.** Either:
1. Implement it fully, OR
2. Don't add it to the codebase

This applies to all scopes (Small/Medium/Large) and all project types.

### Testing
- Write tests before implementation (TDD)
- NO MOCKING in integration tests - use real infrastructure
- Test at all breakpoints (mobile/tablet/desktop)

### Documentation
- Document work in markdown as you go
- Use numbered format: `01-...`, `02-...`, etc.
- Include file:line references for code locations

### Security
- Never commit secrets (.env, credentials)
- Validate at system boundaries (user input, external APIs)
- Check for OWASP top 10 vulnerabilities

---

## MCP Integrations

### Base (from everything-claude-code)
- GitHub
- Supabase
- Vercel
- Railway

### Additional (configured in .claude/mcp-configs/)
- AWS (S3, Lambda, EC2)
- GCP (Cloud Storage, Cloud Functions, Compute Engine)
- Azure (Blob Storage, Azure Functions, VMs)
- Linear (Issue tracking)
- Jira (Sprint management)

See `.claude/mcp-configs/` for setup instructions.

---

## Skills Library

### Available Categories
| Category | Description |
|----------|-------------|
| 06-cheatsheets | Quick reference patterns |
| 07-development-guides | Development practices |
| 09-workflow-patterns | Reusable workflow designs |
| 10-deployment-git | Docker + Git workflows |
| 11-frontend-integration | React/Vue patterns |
| 12-testing-strategies | Testing methodologies |
| 15-error-troubleshooting | Common errors & solutions |
| 17-gold-standards | Compliance standards |

---

## Project Setup Template

When starting a new project, configure these in `instructions.md`:
- **Scope**: Small / Medium / Large
- **Final Product**: Web / Mobile / Desktop / Open-Ended
- **Commercial or Personal Use**
- **Objective/Use-Case**
- **Data Sources**
- **Visual Style**
- **External Tool Integration**
- **Existing Product Reference**

---

## Quick Commands Reference

```bash
# Development
/tdd              # Start test-driven development
/plan             # Plan implementation
/code-review      # Review code quality
/orchestrate      # Multi-agent orchestration

# Testing
/e2e              # Generate E2E tests
/verify           # Run verification loop
/test-coverage    # Analyze test coverage
/eval             # Run evaluation harness

# Maintenance
/build-fix        # Fix build errors
/refactor-clean   # Remove dead code
/update-codemaps  # Update code maps
/update-docs      # Update documentation

# Learning & State
/learn            # Extract patterns from session
/checkpoint       # Save verification state
/setup-pm         # Configure package manager
```

---

## Environment Setup

### Must Do Before Starting
1. Set up isolated environments (venv for Python, node for Node.js)
2. Enable turbo-all and SafeToAutoRun for common commands
3. Check available skills/agents before implementing complex changes
4. Document all work in markdown files as you progress
