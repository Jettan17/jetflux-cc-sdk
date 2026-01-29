## What's New in v4.0

### New Command: `/run`
Execute implementation plans with smart TDD integration. Reads plans created by `/design` and automatically applies TDD workflow when recommended.

```bash
/run                # Execute current plan
/run --force-tdd    # Force TDD even if plan says No
/run --no-tdd       # Skip TDD even if plan says Yes
```

### Restructured Workflow

| Before (v3.2) | After (v4.0) |
|---------------|--------------|
| `/design` → `/tdd` → `/verify` | `/design` → `/run` → `/tdd` → `/verify` |

### Command Changes

| Command | Change |
|---------|--------|
| `/design` | Saves plans to `.claude/plans/current.md`, does NOT implement |
| `/run` | **NEW** - Executes plans with smart TDD |
| `/tdd` | Test utilities only - runs tests, no implementation |
| `/checkpoint` | Added `--push` flag, saves to `docs/checkpoints/` |

### TDD Recommendation Logic

Plans now include "TDD Recommended: Yes/No" based on task type:
- **Yes**: New features, bug fixes, refactoring
- **No**: Documentation, config changes, UI styling only

### Files Changed
- Added `.claude/commands/run.md`
- Added `.claude/plans/` directory for plan storage
- Updated `/design`, `/tdd`, `/checkpoint` commands
- Updated all documentation (CLAUDE.md, README.md, instructions.md)
