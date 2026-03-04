---
description: Initialize a new project with JetFlux SDK (full setup)
origin: "jetflux-original"
created: "2026-01-26"
---

# /sdk - Initialize or Update Project

Create a new project with JetFlux SDK, or update an existing project's SDK files.

## Usage

```bash
/sdk                           # Interactive setup in current directory
/sdk my-project                # Create new project in ./my-project
/sdk ../projects/my-app        # Create at specific path
/sdk --update                  # Update SDK files in current project
/sdk my-project --update       # Update SDK files in existing project
```

## Mode Detection

The command automatically detects whether to run in **new project** or **update** mode:

| Condition | Mode | Behavior |
|-----------|------|----------|
| Directory doesn't exist | New | Full initialization |
| Directory exists but no `.claude/` folder | New | Initialize in existing directory |
| Directory has `.claude/` folder | Update | Refresh SDK files only |
| `--update` flag provided | Update | Force update mode |

## What This Does

### For NEW Projects

**IMPORTANT:** `/sdk` only creates structure and a plan. It does NOT implement any code, install dependencies, or scaffold frameworks. Implementation happens later with `/run`.

#### Step 1: Gather Project Settings

Use AskUserQuestion to collect (max 4 questions per call):

**Batch 1:**
| Setting | Options |
|---------|---------|
| **Scope** | Small / Medium / Large |
| **Product Type** | Web / Mobile / Desktop / CLI |
| **Usage** | Commercial / Personal |
| **Connection Type** | Local / Public |

**Batch 2:**
| Setting | Options |
|---------|---------|
| **Tech Stack** | Next.js / Astro / React / Vue / Plain HTML / Python / Flutter |
| **Package Manager** | pnpm (Recommended) / npm / yarn / bun / pip+uv |
| **Visual Style** | Minimal / Dark / Colorful / Professional (skip if CLI/backend) |

Then ask free-text questions (as regular questions, not AskUserQuestion):
- Project name / directory path (e.g. `../my-project`)
- Objective/Use-case and any requirements the user has already described
- Data sources (optional)
- External integrations (optional)

#### Step 2: Create Directory + SDK Files

Create the project directory and copy SDK files:

```bash
mkdir -p [project-path]

# Copy .claude folder, CLAUDE.md from SDK
cp -r [sdk]/.claude [project]/.claude
cp [sdk]/CLAUDE.md [project]/CLAUDE.md
cp [sdk]/project-settings.md [project]/project-settings.md
```

#### Step 3: Create Skeleton Structure

Create only the top-level folders and config/boilerplate files appropriate for the tech stack. Do NOT write any implementation code.

**Python projects:**
```
src/[package-name]/
  __init__.py          # empty
  [module]/
    __init__.py        # empty
tests/
  phase1/
    __init__.py
  phase2/
    __init__.py
  ...
docs/
  plan.md              # generated in Step 5
pyproject.toml         # with dependencies listed (not installed)
.env.example           # token/key placeholders
.gitignore
README.md              # status table, usage placeholder
```

**Node/Web projects:**
```
src/
  [relevant dirs based on stack]/
docs/
  plan.md
package.json           # with scripts and deps listed (not installed)
.env.example
.gitignore
README.md
```

**Rules:**
- Every `__init__.py` or `index.ts` is empty — no implementation
- `pyproject.toml` / `package.json` lists dependencies but does NOT run install
- No framework CLI scaffolding (`create-next-app`, `flutter create`, etc.)

#### Step 4: Update project-settings.md

Replace the Project Settings section with gathered values:

```markdown
# Project Settings

## Scope
[Selected scope]

## Final Product
[Selected product type] - [Selected tech stack]

## Commercial or Personal Use
[Selected usage]

## Local or Public Connection
[Selected connection type]

## Package Manager
[Selected package manager]

## Objective/Use-Case
[User's objective]

## Visual Style
[Selected style or "N/A"]

## Data Sources
[User's data sources or "None specified"]

## External Tool Integration
[User's integrations or "None initially"]
```

#### Step 5: Generate docs/plan.md

Create a phased implementation plan based on the project requirements. Each phase must:
- Be independently testable (the user can stop after any phase and verify it works)
- End with a concrete **Test Checkpoint** showing exact commands to verify completion
- Build on the previous phase (no phase assumes future phases exist)

**Plan structure:**

```markdown
# [Project Name] — Implementation Plan

## PHASE 1A — [Name]
**Days X–Y | ~Z hrs**

### Tasks
- [ ] ...

### Files Created
- `path/to/file.py` — purpose

### Test Checkpoint ✓
\`\`\`bash
[exact command to verify this phase is done]
# PASS: [what success looks like]
\`\`\`

---

## PHASE 1B — [Name]
...
```

Segment phases to match the project scope:
- **Small**: 2–4 phases total
- **Medium**: 6–10 phases total
- **Large**: 10–15 phases total

#### Step 6: Generate README.md

Create a minimal README with:
- One-line description
- Status table listing all phases (all "⬜ Not started")
- Installation placeholder (fill in after `/run`)
- Usage placeholder

#### Step 7: Initialize Git

```bash
git init
git add .
git commit -m "Initial commit: Project setup with JetFlux SDK"
```

---

### For EXISTING Projects (Update Mode)

When updating an existing project's SDK files:

#### Step 1: Detect SDK Location

Find the JetFlux SDK source directory. Check in order:
1. Environment variable `JETFLUX_SDK_PATH`
2. `~/.jetflux-sdk/` (default installation)
3. Sibling directory `../jetflux-cc-sdk/`
4. Ask user for SDK location if not found

#### Step 2: Backup Current SDK Files (Optional)

Ask user if they want to backup before updating:
```bash
# Create timestamped backup
Copy-Item -Path ".claude" -Destination ".claude.backup.YYYYMMDD" -Recurse
```

#### Step 3: Update SDK Files (Existing Files Only)

**IMPORTANT:** The target project's directory structure is the source of truth. Only update files that already exist in the target project - do NOT add new files from the SDK.

This ensures that files intentionally removed from a project (e.g., language-specific commands, e2e, no-stubs) are not re-added during updates.

**Update Algorithm:**

```bash
# PowerShell (Windows)

# 1. Get list of existing files in target project's .claude folder
$existingFiles = Get-ChildItem -Path ".claude" -Recurse -File |
    ForEach-Object { $_.FullName.Replace((Get-Location).Path + "\.claude\", "") }

# 2. For each existing file, update it from SDK source (if SDK has it)
foreach ($file in $existingFiles) {
    $sdkFile = Join-Path "[sdk]/.claude" $file
    $targetFile = Join-Path ".claude" $file

    if (Test-Path $sdkFile) {
        Copy-Item $sdkFile $targetFile -Force
    }
}

# 3. Update CLAUDE.md (always update, it's the master directives)
Copy-Item "[sdk]/CLAUDE.md" "CLAUDE.md" -Force

# PRESERVE project-settings.md - don't overwrite (contains project settings)
```

**Bash/Unix equivalent:**
```bash
# Find existing files and update only those
find .claude -type f | while read target_file; do
    relative_path="${target_file#.claude/}"
    sdk_file="[sdk]/.claude/$relative_path"

    if [ -f "$sdk_file" ]; then
        cp "$sdk_file" "$target_file"
    fi
done

# Update CLAUDE.md
cp "[sdk]/CLAUDE.md" "CLAUDE.md"
```

**What this means:**
- ✅ Files that exist in target AND SDK → Updated
- ✅ Files that exist only in target (custom) → Preserved unchanged
- ❌ Files that exist only in SDK (new) → NOT added
- ✅ `project-settings.md` → Always preserved (never overwritten)

**Important:** `project-settings.md` is NOT overwritten during updates to preserve project settings.

#### Step 4: Show Update Summary

Display what was updated:
```
SDK files updated successfully!

Updated (existing files only):
- .claude/commands/ (X files updated)
- .claude/agents/ (X files updated)
- .claude/mcp-configs/ (X files updated)
- CLAUDE.md

Preserved (project-specific):
- project-settings.md
- Any custom files not in SDK

Skipped (not in target project):
- [List any SDK files not present in target]

SDK Version: [commit hash or date]
```

---

## Output

After completion, display:

```
Project initialized!

Location: [full path]
Tech Stack: [stack]
Scope: [scope]
Phases: [N phases in docs/plan.md]

Structure created — no code implemented yet.

Next steps:
1. cd [project-path]
2. Review docs/plan.md
3. Run /run to start Phase 1A

Available commands:
- /run      - Implement the plan (Phase by Phase)
- /tdd      - Run tests after each phase
- /verify   - Full verification
```

## Arguments

- `[path]` - Optional. Project directory path. Defaults to current directory.
- `--update` - Force update mode (refresh SDK files in existing project)
- `--no-git` - Skip git initialization (new projects only)
- `--no-backup` - Skip backup prompt during updates
- `--pm <manager>` - Set package manager directly (pnpm/npm/yarn/bun/pip)
- `--pm detect` - Auto-detect package manager from lockfiles

## Agent Escalation

| Condition | Agent | Purpose |
|-----------|-------|---------|
| Tech stack selection | **framework-advisor** | Help choose appropriate stack |
| Complex requirements | **requirements-analyst** | Break down project scope |

## Examples

```bash
# NEW PROJECT: Create in a sibling directory (recommended)
/sdk ../my-portfolio

# NEW PROJECT: Interactive (will ask for path)
/sdk

# UPDATE: Refresh SDK files in current project
/sdk --update

# UPDATE: Refresh SDK files in specific project
/sdk ../my-project --update

# UPDATE: Quick update without backup prompt
/sdk --update --no-backup

# NEW PROJECT: Specify package manager directly
/sdk ../my-project --pm pnpm

# NEW PROJECT: Auto-detect package manager from existing lockfiles
/sdk --pm detect
```

## Notes

- Command auto-detects new vs existing projects based on `.claude/` folder presence
- For new projects: gathers settings → creates skeleton structure → generates plan → stops. No code is implemented.
- For existing projects: updates SDK files only, preserves `project-settings.md`
- Never run framework CLIs (`create-next-app`, `flutter create`, etc.) — structure is created manually
- Never install dependencies — user installs after reviewing the plan
- Always verify `project-settings.md` and `docs/plan.md` after initialization

## Next Steps Output

**After completing this command, always display the following block at the end of your output:**

```
---
Next: /design - Plan your first feature
 Or: /wordlist - Build domain vocabulary for precise prompting
---
```
