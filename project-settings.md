# Project Settings

## Scope

## Final Product

## Commercial or Personal Use

## Objective/Use-Case

## Local or Public Connection

## Package Manager

## Data Sources

## Visual Style

## External Tool Integration

## Existing Product Reference

---

# Creating a New Project

Use AskUserQuestion tool to gather project settings. Do NOT add custom "Other" options - Claude Code adds that automatically.

## Questions to Ask (use AskUserQuestion)

### Question 1: Scope
Options (2-4 max, no "Other"):
- **Small**: Quick tasks, use existing solutions, minimal planning
- **Medium**: Present plan before proceeding, moderate detail
- **Large**: Deep analysis, detailed architecture, comprehensive planning

### Question 2: Final Product
Options:
- **Web**: Browser-based application
- **Mobile**: iOS/Android app
- **Desktop**: Native desktop application

### Question 3: Usage Type
Options:
- **Personal**: Local-first, can use open source freely
- **Commercial**: Production-ready, scalable, with deployment

### Question 4: Connection Type
Options:
- **Public**: Can use internet services and APIs
- **Local**: Offline, local models and databases only

### Question 5: Visual Style (if applicable)
Options (pick 3-4, Claude Code adds "Other"):
- **Modern**: Clean, contemporary (bryanminear.com)
- **High-Key**: Bold, vibrant (landonorris.com, animejs.com)
- **Minimalist**: Simple, focused (kickpush.co, dau.lt)
- **Product**: Professional SaaS (slack.com)
- **Artsy**: Creative, expressive (justinjackson.ca)

### Free-text Questions (ask separately, not with AskUserQuestion)
After the above, ask these as regular questions:
- **Objective**: "What is the main use-case? Describe how users will use the product."
- **Data Sources**: "Any specific data sources? (optional)"
- **Integrations**: "Any external tools or APIs to integrate? (optional)"
- **Reference**: "Any existing products to reference? (optional)"

## After Gathering Settings
Update the "Project Settings" section at the top of this file with the answers.

---

# Behavior by Scope

**Small Scope:**
- Parsimonious approach
- Seek existing solutions first
- Minimal documentation

**Medium Scope:**
- Present plan before implementation
- Moderate detail in architecture

**Large Scope:**
- Deep analysis (use ultrathink-analyst)
- Detailed architecture decisions
- Comprehensive documentation

---

# Behavior by Usage Type

**Personal Use:**
- Local-first, deploy later
- Can use open source freely
- Fork and copy from other sources (non-commercial)

**Commercial Use:**
- Research value propositions and UNIQUE SELLING POINTS
- Scrutinize and critique scenarios to improve the solution
- Evaluate with AAA framework:
  - Automate: Reduce operational costs
  - Augment: Reduce decision-making costs
  - Amplify: Reduce expertise costs (for scaling)
- Features should cover network behaviors:
  - Accessibility: Easy for users to complete transactions
  - Engagement: Useful information for transactions
  - Personalization: Curated information for intended use
  - Connection: Information sources connected to platform
  - Collaboration: Producers and consumers can work together
- Production deployment priority
