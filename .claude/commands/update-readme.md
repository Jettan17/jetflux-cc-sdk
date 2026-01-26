---
description: Generate README from project codebase analysis
origin: "jetflux-original"
created: "2026-01-26"
---

# /update-readme - Generate Project README

Analyze the current project's codebase and generate/update its README.md.

## Usage

```bash
/update-readme              # Full README generation
/update-readme preview      # Preview only, don't write
/update-readme section X    # Update specific section only
```

## What This Does

### 1. Detect Project Type & Stack

Check for project markers:

| File | Stack Detection |
|------|-----------------|
| `package.json` | Node.js, check dependencies for React/Next.js/Vue/etc. |
| `requirements.txt` / `pyproject.toml` | Python |
| `pubspec.yaml` | Flutter/Dart |
| `go.mod` | Go |
| `Cargo.toml` | Rust |
| `pom.xml` / `build.gradle` | Java |

### 2. Analyze Project Structure

Scan the codebase for:

- **Source directories**: `src/`, `lib/`, `app/`, `packages/`
- **Entry points**: `index.ts`, `main.py`, `main.go`, etc.
- **API routes**: `app/api/`, `pages/api/`, `routes/`
- **Components**: `components/`, `views/`, `screens/`
- **Services**: `services/`, `utils/`, `lib/`
- **Configuration**: `.env.example`, `docker-compose.yml`, `Dockerfile`
- **Tests**: `tests/`, `__tests__/`, `*.test.*`, `*.spec.*`

### 3. Extract Documentation Sources

Pull information from:

- **Existing README.md**: Project name, description (preserve if good)
- **package.json**: `name`, `description`, `scripts`, `dependencies`
- **.env.example**: Environment variables with comments
- **CLAUDE.md / instructions.md**: Project context and objectives
- **Dockerfile**: Deployment hints
- **tsconfig.json / jsconfig.json**: Build configuration

### 4. Generate README Sections

```markdown
# {Project Name}

{Description from package.json or existing README}

## Tech Stack

{Badges for detected technologies}

## Prerequisites

- Node.js >= {version from engines or latest LTS}
- {Package manager} (npm/pnpm/yarn/bun)
- {Other requirements}

## Getting Started

### Installation

```bash
{package manager} install
```

### Environment Setup

Copy `.env.example` to `.env` and configure:

| Variable | Description | Required |
|----------|-------------|----------|
| {var} | {description from comments} | {yes/no} |

### Development

```bash
{dev command from scripts}
```

## Available Scripts

| Script | Description |
|--------|-------------|
| {script} | {description or inferred purpose} |

## Project Structure

```
{tree of main directories}
```

## API Reference

{If API routes detected, list endpoints}

## Deployment

{If Docker/K8s files detected, include deployment section}

## Contributing

{Standard contribution guidelines}

## License

{From package.json or existing README}
```

### 5. Preview & Confirm

Before writing:
1. Show generated README preview
2. Highlight what changed from existing README
3. Ask user to confirm
4. Preserve sections marked with `<!-- keep -->` tags

## Preserving Custom Sections

Mark sections you want to keep unchanged:

```markdown
<!-- keep -->
## Custom Section
This content won't be overwritten by /update-readme
<!-- /keep -->
```

## Arguments

- `preview` - Show generated README without writing
- `section <name>` - Update only a specific section
- `force` - Write without confirmation prompt

## Examples

```bash
# Generate full README for a new project
/update-readme

# Preview what would be generated
/update-readme preview

# Update only the scripts section
/update-readme section scripts

# Force update without confirmation
/update-readme force
```

## Agent Escalation

This command automatically escalates to specialized agents when:

| Condition | Agent | Purpose |
|-----------|-------|---------|
| Complex project structure | **architect** | Understand architecture for accurate documentation |
| API documentation needed | **documentation-validator** | Validate API docs match implementation |

### Escalation Triggers
- **architect**: Use for monorepos, microservices, or complex architectures
- **documentation-validator**: Use to ensure generated docs are accurate