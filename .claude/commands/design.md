---
description: Restate requirements, assess risks, and create step-by-step implementation plan. Saves plan to file for /run execution.
ecc_base_version: "5230892"
last_synced: "2026-01-28"
customizations: "Plan-only mode, saves to .claude/plans/current.md, includes TDD recommendation"
---

# /design - Implementation Planning

This command creates a comprehensive implementation plan and saves it for later execution with `/run`. **Does NOT implement code.**

## What This Command Does

1. **Restate Requirements** - Clarify what needs to be built
2. **Identify Risks** - Surface potential issues and blockers
3. **Create Step Plan** - Break down implementation into phases
4. **Recommend TDD** - Determine if test-driven development is appropriate
5. **Save Plan** - Write plan to `.claude/plans/current.md`
6. **Stop** - Wait for user to run `/run` to execute

## When to Use

Use `/design` when:
- Starting a new feature
- Making significant architectural changes
- Working on complex refactoring
- Multiple files/components will be affected
- Requirements are unclear or ambiguous

## How It Works

The planner agent will:

1. **Analyze the request** and restate requirements in clear terms
2. **Break down into phases** with specific, actionable steps
3. **Identify dependencies** between components
4. **Assess risks** and potential blockers
5. **Determine TDD recommendation** based on task type
6. **Save plan** to `.claude/plans/current.md`
7. **Display summary** and prompt user to run `/run`

## Plan File Format

Plans are saved to `.claude/plans/current.md` with this structure:

```markdown
# Implementation Plan: [Title]

Created: [timestamp]
Status: pending

## Requirements
[restated requirements in clear terms]

## Implementation Phases

### Phase 1: [Name]
- [ ] Step 1
- [ ] Step 2

### Phase 2: [Name]
- [ ] Step 1
- [ ] Step 2

## Dependencies
- [list of dependencies]

## Risks
- HIGH: [description]
- MEDIUM: [description]
- LOW: [description]

## TDD Recommended: Yes/No
**Reason:** [explanation of why TDD is or isn't recommended]

## Test Strategy

### Detected Code Types
| Phase | Files | Code Type | Primary Tests | Secondary Tests |
|-------|-------|-----------|---------------|-----------------|
| 1 | lib/utils.ts | Utility | Unit | - |
| 2 | components/Button.tsx | UI Component | Unit | E2E |
| 3 | api/users.ts | API Endpoint | Integration (NO MOCK) | - |

### Test Execution Plan
1. Unit Tests (run first, fastest feedback)
2. Integration Tests (NO MOCKING - real Docker services)
3. E2E Tests (run last, verify user journeys)
```

## Code Type Detection Heuristics

The planner automatically detects code types based on file paths:

| Path Pattern | Code Type | Primary Tests | Secondary Tests |
|--------------|-----------|---------------|-----------------|
| `components/`, `ui/` | UI Component | Unit | E2E |
| `api/`, `handlers/`, `routes/` | API Endpoint | Integration (NO MOCK) | Unit |
| `utils/`, `lib/`, `helpers/` | Utility | Unit | - |
| `services/` | Service | Integration | Unit |
| `models/`, `db/`, `prisma/` | Data Layer | Integration | - |
| `pages/`, `app/` | Page/Route | E2E | Unit |
| `hooks/` | React Hook | Unit | - |
| `middleware/` | Middleware | Integration | Unit |

### Test Type Definitions

| Test Type | Purpose | Mocking Policy |
|-----------|---------|----------------|
| **Unit** | Test isolated functions/components | Mocking ALLOWED |
| **Integration** | Test service interactions | NO MOCKING - real services |
| **E2E** | Test user journeys | NO MOCKING - real infrastructure |

## TDD Recommendation Logic

| Scenario | TDD Recommended | Reason |
|----------|-----------------|--------|
| New feature with code | **Yes** | Tests define expected behavior |
| Bug fix | **Yes** | Test reproduces bug first |
| Code refactoring | **Yes** | Tests ensure behavior preserved |
| Documentation only | No | No code to test |
| Architecture decisions | No | Planning phase, no implementation |
| Config changes | No | Usually validated by running |
| UI styling only | No | Visual changes, hard to test |
| Database migrations | No | Usually tested by running migration |

## Example Usage

```
User: /design I need to add real-time notifications when markets resolve

Agent (planner):
# Implementation Plan: Real-Time Market Resolution Notifications

## Requirements Restatement
- Send notifications to users when markets they're watching resolve
- Support multiple notification channels (in-app, email, webhook)
- Ensure notifications are delivered reliably
- Include market outcome and user's position result

## Implementation Phases

### Phase 1: Database Schema
- [ ] Add notifications table
- [ ] Add user_notification_preferences table
- [ ] Create indexes for performance

### Phase 2: Notification Service
- [ ] Create notification service in lib/notifications.ts
- [ ] Implement notification queue
- [ ] Add retry logic
- [ ] Create notification templates

### Phase 3: Integration Points
- [ ] Hook into market resolution logic
- [ ] Query affected users
- [ ] Enqueue notifications

### Phase 4: Frontend Components
- [ ] Create NotificationBell component
- [ ] Add NotificationList modal
- [ ] Implement real-time updates
- [ ] Add preferences page

## Dependencies
- Redis (for queue)
- Email service (SendGrid/Resend)
- Supabase real-time subscriptions

## Risks
- HIGH: Email deliverability (SPF/DKIM required)
- MEDIUM: Performance with 1000+ users per market
- MEDIUM: Notification spam if markets resolve frequently

## TDD Recommended: Yes
**Reason:** This is a new feature with significant code changes across multiple files. Tests will ensure notification logic works correctly before deployment.

---

Plan saved to `.claude/plans/current.md`

Run `/run` to execute this plan.
```

## Modifying Plans

Before running `/run`, you can:
- Edit `.claude/plans/current.md` directly
- Run `/design` again with modifications: `/design modify: skip email for now`
- Ask for clarification: "What about handling rate limits?"

## Integration with Other Commands

```
/design "Add feature"  →  Creates plan, saves to file
/run                   →  Executes plan (with TDD if recommended)
/tdd                   →  Run tests only (after implementation)
/verify                →  Full verification
```

## Agent Escalation

This command automatically escalates to specialized agents when:

| Condition | Agent | Purpose |
|-----------|-------|---------|
| Complex requirements, systemic issues | **ultrathink-analyst** | Deep failure analysis, comprehensive requirement breakdown |
| Architecture decisions needed | **requirements-analyst** | ADR creation, systematic requirements breakdown |
| Technology selection required | **framework-advisor** | Tech stack decisions, framework recommendations |

### Escalation Triggers
- **ultrathink-analyst**: Use when task touches 3+ components, has unclear failure modes, or needs risk analysis
- **requirements-analyst**: Use when creating new architecture, making significant design decisions, or need formal ADRs
- **framework-advisor**: Use when choosing between frameworks, libraries, or implementation approaches

## Related Commands

- `/run` - Execute the saved plan
- `/tdd` - Run tests (after implementation)
- `/verify` - Full verification after implementation
- `/code-review` - Review completed implementation
