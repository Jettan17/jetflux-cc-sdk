---
description: Execute the current design plan with smart TDD integration
ecc_base_version: "5230892"
last_synced: "2026-01-28"
customizations: "New command for plan execution"
---

# /run - Execute Plan

Executes the implementation plan saved by `/design`. Automatically applies TDD workflow when recommended.

## What This Command Does

1. **Read Plan** - Load plan from `.claude/plans/current.md`
2. **Validate Plan** - Check plan exists and is well-formed
3. **Check TDD Recommendation** - Read the TDD recommendation from the plan
4. **Execute Implementation:**
   - If TDD Recommended = Yes: Full TDD cycle (RED → GREEN → REFACTOR)
   - If TDD Recommended = No: Direct implementation
5. **Update Plan Status** - Mark phases as completed
6. **Verify** - Ensure implementation matches plan requirements

## Usage

```bash
/run                    # Execute current plan (respects TDD recommendation)
/run --force-tdd        # Force TDD even if plan says No
/run --no-tdd           # Skip TDD even if plan says Yes
/run --phase 2          # Start from specific phase
/run --dry-run          # Show what would be done without executing
```

## How It Works

### With TDD (Recommended = Yes)

For each implementation phase:

```
1. Write failing tests (RED)
   - Create test files for the phase
   - Define expected behavior
   - Run tests → verify they FAIL

2. Implement minimal code (GREEN)
   - Write just enough code to pass tests
   - Run tests → verify they PASS

3. Refactor (REFACTOR)
   - Improve code quality
   - Keep tests passing
   - Check coverage

4. Mark phase complete
   - Update plan status
   - Move to next phase
```

### Without TDD (Recommended = No)

For each implementation phase:

```
1. Implement changes directly
   - Follow plan steps
   - Verify build succeeds

2. Manual verification
   - Check changes work as expected
   - Run any existing tests

3. Mark phase complete
   - Update plan status
   - Move to next phase
```

## Error Handling

| Condition | Behavior |
|-----------|----------|
| No plan exists | Error: "No plan found. Run `/design` first." |
| Plan is stale (>24h) | Warning: "Plan is X hours old. Continue? (y/n)" |
| Tests fail | Stop and report: "Tests failing. Fix before continuing." |
| Build fails | Stop and suggest: "Build error. Run `/build-fix`." |
| Phase incomplete | Allow retry: "Phase X incomplete. Retry? (y/n)" |

## Example: TDD Execution

```
User: /run

Agent:
Reading plan from .claude/plans/current.md...

# Executing: Real-Time Market Resolution Notifications
TDD Recommended: Yes

## Phase 1: Database Schema (TDD)

### RED: Writing failing tests...
- tests/db/notifications.test.ts
  - should create notifications table
  - should create user_notification_preferences table
  - should have required indexes

Running tests... 3 failing ✗

### GREEN: Implementing schema...
- migrations/001_notifications.sql
- lib/db/notifications.ts

Running tests... 3 passing ✓

### REFACTOR: Cleanup...
- Added TypeScript types
- Extracted constants

Running tests... 3 passing ✓

Phase 1 complete ✓

## Phase 2: Notification Service (TDD)

### RED: Writing failing tests...
[continues...]
```

## Example: Non-TDD Execution

```
User: /run

Agent:
Reading plan from .claude/plans/current.md...

# Executing: Update README Documentation
TDD Recommended: No (documentation only)

## Phase 1: Update Feature List

Implementing...
- Updated README.md with new features
- Added usage examples
- Fixed outdated links

Build check... ✓

Phase 1 complete ✓

## Phase 2: Add API Documentation

Implementing...
- Created docs/api.md
- Added endpoint documentation
- Included request/response examples

Build check... ✓

Phase 2 complete ✓

All phases complete. Run `/verify` to validate.
```

## Plan Status Updates

The `/run` command updates `.claude/plans/current.md` as it executes:

```markdown
# Implementation Plan: [Title]

Created: 2026-01-28T10:00:00Z
Status: in_progress
Started: 2026-01-28T10:30:00Z

## Implementation Phases

### Phase 1: Database Schema ✓
Completed: 2026-01-28T10:45:00Z
- [x] Add notifications table
- [x] Add user_notification_preferences table
- [x] Create indexes for performance

### Phase 2: Notification Service (in progress)
Started: 2026-01-28T10:46:00Z
- [x] Create notification service
- [ ] Implement notification queue
- [ ] Add retry logic
```

## Flags

| Flag | Description |
|------|-------------|
| `--force-tdd` | Apply TDD workflow even if plan recommends No |
| `--no-tdd` | Skip TDD workflow even if plan recommends Yes |
| `--phase N` | Start execution from phase N |
| `--dry-run` | Preview execution plan without making changes |
| `--continue` | Resume from last incomplete phase |

## Integration with Other Commands

```
/design "Add feature"  →  Creates plan, saves to file
/run                   →  Executes plan (you are here)
/tdd                   →  Run tests (verification)
/verify                →  Full verification
/code-review           →  Quality review
```

## Agent Escalation

| Condition | Agent | Purpose |
|-----------|-------|---------|
| React/Next.js implementation | **ui-engineer** | React 19, Next.js 15 patterns |
| Flutter implementation | **flutter-specialist** | Mobile patterns |
| Test failures | **intermediate-reviewer** | Diagnose issues |
| Build errors | **build-error-resolver** | Fix compilation |
| Security concerns | **security-auditor** | Security review |

## Related Commands

- `/design` - Create a plan (prerequisite)
- `/tdd` - Run tests after implementation
- `/build-fix` - Fix build errors if they occur
- `/verify` - Full verification after completion
- `/checkpoint` - Save progress state
