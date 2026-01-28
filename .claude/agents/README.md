# Claude Code SDK Subagents

This directory contains specialized subagents for the Claude Code SDK development environment.

## Available Agents (13 total)

| Agent | Purpose | When to Use |
|-------|---------|-------------|
| **deep-reflector** | Session analysis and learning capture | `/learn` command, pattern extraction |
| **deployment-specialist** | Docker/Kubernetes deployment | Production deployments, CI/CD setup |
| **documentation-validator** | Documentation validation | Testing code examples, doc accuracy |
| **flutter-specialist** | Flutter mobile/desktop apps | Cross-platform mobile development |
| **framework-advisor** | Framework selection guidance | Technology stack decisions |
| **gh-manager** | GitHub project management | Issue tracking, project boards, PRs |
| **gold-standards-validator** | Compliance checking | Code validation, standards enforcement |
| **intermediate-reviewer** | Checkpoint reviews | Progress validation, milestone critiques |
| **requirements-analyst** | Requirements breakdown | ADRs, systematic analysis |
| **security-auditor** | Security analysis | Vulnerability scanning, OWASP Top 10 |
| **todo-manager** | Task management | Todo lists, project tracking |
| **ui-engineer** | UI/UX specialist | React, accessibility, design systems |
| **ultrathink-analyst** | Deep failure analysis | Complex features, risk analysis |

---

## Workflow Phases

### Phase 1: Analysis & Planning
```
1. Run /design to create implementation plan
2. > Use ultrathink-analyst for complex requirement analysis
3. > Use requirements-analyst for systematic breakdown
4. > Use framework-advisor for technology decisions
5. > Use todo-manager to create task breakdown
```

### Phase 2: Implementation
```
1. Run /run to execute the plan (uses TDD when recommended)
2. > Use ui-engineer for frontend components
3. > Use flutter-specialist for mobile components
4. > Use gold-standards-validator to ensure compliance
5. > Use intermediate-reviewer to review progress
```

### Phase 3: Testing & Quality
```
1. Run /tdd to run all tests
2. Run /tdd e2e for end-to-end tests
3. Run /tdd coverage to check coverage gaps
4. > Use documentation-validator to verify docs
5. > Use todo-manager to update task status
```

### Phase 4: Deployment
```
1. Run /deploy for Docker/Kubernetes setup
2. > Use deployment-specialist for production config
```

### Phase 5: Release
```
1. Run /code-review for final quality check
2. > Use security-auditor for security scan
3. > Use intermediate-reviewer for final critique
4. > Use gh-manager to sync with GitHub Projects
```

---

## Quick Debugging

```
When facing issues:
1. > Use ultrathink-analyst for deep analysis
2. > Use ui-engineer for frontend issues
3. > Use flutter-specialist for mobile issues
4. > Use deployment-specialist for infrastructure issues
```

---

## Agent Files

All agent files are in `.claude/agents/`:

| File | Agent |
|------|-------|
| `deep-reflector.md` | Session analysis and learning capture |
| `deployment-specialist.md` | Docker/Kubernetes deployment |
| `documentation-validator.md` | Documentation validation |
| `flutter-specialist.md` | Flutter mobile/desktop apps |
| `framework-advisor.md` | Framework selection guidance |
| `gh-manager.md` | GitHub project management |
| `gold-standards-validator.md` | Compliance checking |
| `intermediate-reviewer.md` | Checkpoint reviews |
| `requirements-analyst.md` | Requirements breakdown |
| `security-auditor.md` | Security analysis |
| `todo-manager.md` | Task management |
| `ui-engineer.md` | UI/UX specialist |
| `ultrathink-analyst.md` | Deep failure analysis |
