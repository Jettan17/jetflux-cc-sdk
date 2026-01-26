---
name: gold-no-stubs
description: "Mandatory standard requiring complete implementations. No placeholder text, stub functions, non-functional UI, or incomplete features allowed."
---

# Gold Standard: No Stubs or Placeholders

## The Rule

**Every deliverable must be complete and functional. If a feature isn't ready, don't include it at all.**

This is a **MANDATORY** gold standard. Violations are unacceptable in any codebase.

## Why This Matters

1. **Professionalism**: Placeholder content looks unfinished and unprofessional
2. **User Experience**: Non-functional buttons and empty pages confuse users
3. **Technical Debt**: "TODO" comments often become permanent fixtures
4. **Testing**: Stub functions can't be properly tested
5. **Trust**: Incomplete features erode confidence in the product

## Forbidden Patterns

### UI/Frontend - NEVER Use

```html
<!-- ❌ FORBIDDEN: Placeholder text -->
<h1>Lorem Ipsum Dolor Sit Amet</h1>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit...</p>

<!-- ❌ FORBIDDEN: Coming soon messages -->
<div class="feature-card">
  <h2>Premium Features</h2>
  <p>Coming soon...</p>
  <button disabled>Upgrade (Coming Soon)</button>
</div>

<!-- ❌ FORBIDDEN: Under construction -->
<div class="page-content">
  <h1>🚧 Under Construction 🚧</h1>
  <p>This page is being built. Check back later!</p>
</div>

<!-- ❌ FORBIDDEN: TBD/TODO visible to users -->
<span class="price">$TBD</span>
<p>Description: TODO - add description here</p>

<!-- ❌ FORBIDDEN: Placeholder images -->
<img src="placeholder.jpg" alt="Image coming soon" />
<div class="image-placeholder">[ Image Here ]</div>

<!-- ❌ FORBIDDEN: Non-functional elements -->
<button onclick="alert('Not implemented')">Save</button>
<a href="#">Learn More</a>  <!-- Links to nowhere -->
<form><!-- Empty form with no handler --></form>
```

### Python - NEVER Use

```python
# ❌ FORBIDDEN: Empty pass statements
def process_data(data):
    pass

# ❌ FORBIDDEN: TODO comments as implementation
def calculate_tax(amount):
    # TODO: implement tax calculation
    return 0

# ❌ FORBIDDEN: NotImplementedError as placeholder
def export_report(report):
    raise NotImplementedError("Coming soon")

# ❌ FORBIDDEN: Ellipsis as implementation
def validate_input(data):
    ...

# ❌ FORBIDDEN: Hardcoded sample data
def get_users():
    return [
        {"name": "John Doe", "email": "john@example.com"},
        {"name": "Jane Doe", "email": "jane@example.com"},
    ]  # Should fetch from real source
```

### JavaScript/TypeScript - NEVER Use

```typescript
// ❌ FORBIDDEN: Empty function bodies
function handleSubmit() {}

// ❌ FORBIDDEN: TODO comments as implementation
function calculateDiscount(price: number): number {
  // TODO: implement discount logic
  return price;
}

// ❌ FORBIDDEN: Console.log as implementation
function saveUser(user: User): void {
  console.log("Would save user:", user);
}

// ❌ FORBIDDEN: Throwing not implemented
function exportToPDF(): void {
  throw new Error("Not implemented yet");
}

// ❌ FORBIDDEN: Hardcoded mock data in production
const products = [
  { id: 1, name: "Sample Product", price: 99.99 },
  { id: 2, name: "Another Product", price: 149.99 },
]; // Should come from API
```

## Correct Patterns

### UI/Frontend - DO This

```html
<!-- ✅ CORRECT: Real, meaningful content -->
<h1>Welcome to TaskFlow</h1>
<p>Manage your projects with our intuitive workflow tools.</p>

<!-- ✅ CORRECT: Functional features only -->
<div class="feature-card">
  <h2>Team Collaboration</h2>
  <p>Work together in real-time with shared boards and comments.</p>
  <button onclick="startTrial()">Start Free Trial</button>
</div>

<!-- ✅ CORRECT: Real images or intentionally empty -->
<img src="/images/dashboard-preview.png" alt="Dashboard showing project overview" />

<!-- ✅ CORRECT: All interactive elements work -->
<button onclick="saveDocument()">Save Document</button>
<a href="/docs/getting-started">Learn More</a>
<form onsubmit="handleFormSubmit(event)">...</form>
```

### Python - DO This

```python
# ✅ CORRECT: Fully implemented function
def process_data(data: dict) -> dict:
    """Process and validate input data."""
    if not data:
        raise ValueError("Data cannot be empty")

    validated = validate_schema(data)
    transformed = apply_transformations(validated)
    return {"result": transformed, "status": "success"}

# ✅ CORRECT: Real data fetching
def get_users() -> list[User]:
    """Fetch users from the database."""
    return db.query(User).filter(User.active == True).all()

# ✅ CORRECT: If not ready, don't include at all
# (Simply don't add the function/feature until it's complete)
```

### JavaScript/TypeScript - DO This

```typescript
// ✅ CORRECT: Fully implemented function
function handleSubmit(event: FormEvent): void {
  event.preventDefault();
  const formData = new FormData(event.target as HTMLFormElement);
  submitToAPI(formData);
}

// ✅ CORRECT: Real calculation logic
function calculateDiscount(price: number, discountPercent: number): number {
  if (discountPercent < 0 || discountPercent > 100) {
    throw new Error("Discount must be between 0 and 100");
  }
  return price * (1 - discountPercent / 100);
}

// ✅ CORRECT: Real data from API
async function getProducts(): Promise<Product[]> {
  const response = await fetch("/api/products");
  return response.json();
}
```

## The Decision Framework

When you're tempted to add a stub or placeholder, ask:

```
Is this feature essential for the current deliverable?
│
├── YES → Implement it fully before including
│
└── NO → Don't include it at all
         (Add it in a future iteration when ready)
```

## Exceptions (Very Rare)

The ONLY acceptable exceptions:

1. **Test fixtures**: Mock data in test files is acceptable
2. **Development examples**: Sample data in documentation/tutorials
3. **Explicit user request**: If user specifically asks for a skeleton/scaffold

Even in these cases, mark clearly:
```python
# tests/fixtures/sample_data.py (TEST ONLY - not production)
MOCK_USERS = [...]
```

## Enforcement

### Automated Checks

```bash
# Check for forbidden patterns
grep -r "lorem ipsum" src/
grep -r "coming soon" src/
grep -r "under construction" src/
grep -r "TODO:" src/  # Should be zero in production code
grep -r "pass$" src/*.py  # Empty pass statements
grep -r "NotImplementedError" src/
```

### Code Review Checklist

- [ ] No placeholder text visible in UI
- [ ] No "Coming soon" or "Under construction" messages
- [ ] No empty function bodies
- [ ] No TODO comments in production code
- [ ] All buttons and links are functional
- [ ] All forms have working handlers
- [ ] No hardcoded sample data (except test fixtures)

## Summary

| Situation | Action |
|-----------|--------|
| Feature not ready | Don't include it |
| Need placeholder for layout | Use real content or nothing |
| Function not implemented | Don't add the function yet |
| Page under development | Don't add the route yet |
| Waiting for API | Build with real API or wait |

**Remember: Incomplete is worse than absent.**
