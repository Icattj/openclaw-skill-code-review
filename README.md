---
name: code-review
description: Structured code review with security and quality focus. Use when reviewing code changes, PRs, diffs, or when asked to review someone's code. Covers logic correctness, error handling, security vulnerabilities, performance, and readability. Enforces a systematic checklist approach instead of surface-level "looks good."
---

# Code Review

## The Rule

Never say "looks good" without checking every item below. A proper review catches bugs before users do.

## Review Checklist

### 1. Logic Correctness
- [ ] Does the code do what it claims to do?
- [ ] Are edge cases handled? (empty input, null, zero, negative, max values)
- [ ] Are boundary conditions correct? (off-by-one, inclusive/exclusive)
- [ ] Is the control flow correct? (early returns, loop termination, fallthrough)
- [ ] Are all code paths reachable? (no dead code)

### 2. Error Handling
- [ ] Are errors caught and handled appropriately?
- [ ] Do error messages help with debugging? (not generic "something went wrong")
- [ ] Are async errors handled? (unhandled promise rejections, callback errors)
- [ ] Does it fail gracefully? (not silently swallow errors)
- [ ] Are resources cleaned up on error? (file handles, connections, transactions)

### 3. Security
- [ ] **Injection:** Are inputs sanitized? (SQL, XSS, command injection, path traversal)
- [ ] **Auth:** Are endpoints/functions properly authenticated and authorized?
- [ ] **Secrets:** No hardcoded API keys, passwords, or tokens?
- [ ] **Data exposure:** Are sensitive fields excluded from logs/responses?
- [ ] **CORS/CSP:** Are cross-origin policies correct?
- [ ] **Dependency risk:** Are new dependencies from trusted sources? Known CVEs?

### 4. Performance
- [ ] Are there N+1 query patterns? (DB queries in loops)
- [ ] Are large data sets paginated or streamed?
- [ ] Are expensive operations cached where appropriate?
- [ ] Are there potential memory leaks? (unbounded caches, event listener buildup)
- [ ] Is there unnecessary work? (redundant API calls, duplicate processing)

### 5. Readability & Maintainability
- [ ] Are names clear and descriptive? (no single-letter vars except loops)
- [ ] Is the code self-documenting? (comments explain WHY, not WHAT)
- [ ] Is the function/class size reasonable? (< 50 lines per function)
- [ ] Is there duplication that should be extracted?
- [ ] Would a new developer understand this code?

### 6. Testing
- [ ] Are there tests for new functionality?
- [ ] Do tests cover both happy path and error cases?
- [ ] Are tests independent? (no shared mutable state between tests)
- [ ] Do tests run fast? (no unnecessary I/O, external calls)

## Review Output Format

```markdown
## Code Review: [File/PR name]

### ✅ Good
- [What's done well]

### ⚠️ Issues
1. **[Severity: Critical/Major/Minor]** — [File:Line] [Description]
   Suggestion: [How to fix]

### 💡 Suggestions
- [Optional improvements, not blocking]

### Verdict: [APPROVE / REQUEST CHANGES / NEEDS DISCUSSION]
```

## Severity Guide

- **Critical:** Security vulnerability, data loss, crash in production → must fix
- **Major:** Logic bug, missing error handling, performance issue → should fix
- **Minor:** Style, naming, minor optimization → nice to fix
