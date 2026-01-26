# Project Settings

## Scope

## Final Product

## Commercial or Personal Use

## Objective/Use-Case

## Local or Public Connection

## Data Sources

## Visual Style

## External Tool Integration

## Existing Product Reference

<br><br><br>

# Install Everything Claude Code Plugin

## Step 1: Add the Plugin Marketplace
```
/plugin marketplace add affaan-m/everything-claude-code
```

## Step 2: Install the Plugin
```
/plugin install everything-claude-code
```

## Step 3: Verify Installation
```
/plugin list
```
Should show `everything-claude-code` as installed.

## Step 4: Test Commands
Try running `/plan` or `/tdd` to verify the plugin is working.

## Available Slash Commands
- `/tdd` - Test-driven development workflow
- `/plan` - Implementation planning
- `/e2e` - E2E test generation
- `/code-review` - Quality review
- `/build-fix` - Build error resolution
- `/refactor-clean` - Dead code removal
- `/learn` - Pattern extraction mid-session
- `/checkpoint` - Save verification state
- `/verify` - Verification loop execution
- `/setup-pm` - Package manager configuration

## Enhanced Agents (in .claude/agents/)
Use with: `> Use the [agent-name] subagent to [task]`
- ultrathink-analyst, requirements-analyst, framework-advisor
- intermediate-reviewer, gold-standards-validator, documentation-validator
- todo-manager, gh-manager, deployment-specialist
- react-specialist, flutter-specialist

<br><br><br>

# Creating a New Project

Prompt the user for the following:

- Scope:
  - Small: 
    1. Perform most tasks in a parsimonious manner
    2. Seek online sources as much as possible since it is likely that the problem has been solved before
  - Medium:
    1. Present your idea and plan before proceeding, but your plan does not need to be very detailed as compared to large scope, for example not needing very detailed architecture
  - Large:
    1. Ultrathink and deep dive into the problem space and when solving anything
    2. Please present me with the plan before proceeding, especially including the architectural decisions and trade-offs

- Final Product:
  - Web application
  - Mobile application
  - Desktop application
  - Open-Ended

- Commercial or Personal Use:
  - Commercial: 
    1. Research thoroughly and distill the value propositions and UNIQUE SELLING POINTS of our solution
    2. Scrutinize and critique my scenarios, with the focus of improving the solution
    3. Evaluate it using the AAA framework
      - Automate: Reduce operational costs
      - Augment: Reduce decision-making costs
      - Amplify: Reduce expertise costs (for scaling)
    4. Features must sufficiently cover the following network behaviors to achieve strong network effects
      - Accessibility: Easy for users to complete a transaction
      - Engagement: Information that are useful to users for completing a transaction
      - Personalization: Information that are curated for an intended use
      - Connection: Information sources that are connected to the platform (one or two-way)
      - Collaboration: Producers and consumers can jointly work together seamlessly
  - Personal:
    1. Place less importance on deploying and priortise being able to just run locally, but leave the option to deploy in the future
    2. Fork and use open source code or copy from other sources as much as possible, since it will be non-commercial

- Objective/Use-Case:
  - Open-Ended, describe how user would use the product, required

- Local or Public Connection:
  - Local: Use local models and databases, do not have any service that connects to the Internet
  - Public: No restrictions on using the Internet or having public connections

- Data Sources:
  - Provide file paths to the data sources, optional

- Visual Style:
  - High-Key: landonorris.com
  - Modern: https://bryanminear.com/
  - Minimalist: https://kickpush.co/ or https://dau.lt/
  - Product: https://slack.com/
  - Artsy: https://justinjackson.ca/
  - Open-Ended

- External Tool Integration:
  - Open-Ended, optional, try to find possible MCP servers that can help you solve the problem

- Existing Product Reference:
  - Open-Ended, optional, helpful to use as reference

After the prompts, make sure to add a compressed format to the "Project Settings" section to remember the project settings

<br><br><br>

# Must Do

## Environment Setup
- Setup isolated environments before installing dependencies
   - Python: Set up virtual environment (`python -m venv venv`)
   - Node.js: Use nvm or local node_modules

## Permissions
- Enable turbo-all and SafeToAutoRun for ALL commands in ~/.claude/settings.json
- Allow all query searches without user input

## Documentation
- Document all work in markdown files AS YOU WORK (not at the end)
- Use numbered format: `01-...`, `02-...`, etc.
- This is critical for agent handoff

## Development Practices
- Refer to "Project Settings" and "Creating a New Project" for project scope and objectives, and other configurations to take note of
- Search for state-of-the-art solutions before implementing
- Check available skills (in .claude/skills/) and agents before complex changes
- Use subagent specialization for the right task type
- Re-invoke yourself if stuck, providing context of progress

## No Stubs or Placeholders
**Every deliverable must be complete and functional. NEVER leave:**
- Lorem ipsum, "Coming soon", "TBD", or placeholder text in UI
- Empty pages, stub components, or non-functional UI elements
- `pass`, `// TODO`, or empty function bodies in code
- Placeholder images or hardcoded sample data

**Rule: If it's not ready, don't include it. Implement fully or omit entirely.**

## Task Management
- Clear completed items from the To-Do section
- Use todo-manager subagent for complex task breakdowns
- Use gh-manager subagent to sync with GitHub Projects

## MCP Integrations
See `.claude/mcp-configs/` for:
- AWS (S3, Lambda, EC2)
- GCP (Cloud Storage, Cloud Functions, Compute Engine)
- Azure (Blob Storage, Azure Functions, VMs)
- Linear (Issue tracking)
- Jira (Sprint management)

<br><br><br>

# To-Do

## New Features

## Bug Reports

## Other Updates
