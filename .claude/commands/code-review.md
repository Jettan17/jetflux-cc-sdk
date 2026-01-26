# Code Review

Comprehensive security and quality review of uncommitted changes:

1. Get changed files: git diff --name-only HEAD

2. For each changed file, check for:

**Security Issues (CRITICAL):**
- Hardcoded credentials, API keys, tokens
- SQL injection vulnerabilities
- XSS vulnerabilities  
- Missing input validation
- Insecure dependencies
- Path traversal risks

**Code Quality (HIGH):**
- Functions > 50 lines
- Files > 800 lines
- Nesting depth > 4 levels
- Missing error handling
- console.log statements
- TODO/FIXME comments
- Missing JSDoc for public APIs

**Best Practices (MEDIUM):**
- Mutation patterns (use immutable instead)
- Emoji usage in code/comments
- Missing tests for new code
- Accessibility issues (a11y)

3. Generate report with:
   - Severity: CRITICAL, HIGH, MEDIUM, LOW
   - File location and line numbers
   - Issue description
   - Suggested fix

4. Block commit if CRITICAL or HIGH issues found

Never approve code with security vulnerabilities!

## Agent Escalation

This command automatically escalates to specialized agents when:

| Condition | Agent | Purpose |
|-----------|-------|---------|
| Pattern compliance needed | **gold-standards-validator** | SDK patterns, coding standards enforcement |
| Complex codebase audit | **gold-standards-validator** | Full repository compliance scan |
| Security-critical code | **security-reviewer** | Deep vulnerability analysis |

### Escalation Triggers
- **gold-standards-validator**: Use for SDK compliance, import patterns, node development standards
- **security-reviewer**: Use for auth, payments, PII handling, or external API integrations
