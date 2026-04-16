---
name: sam
description: >
  Ultimate full-project audit skill. Scans entire codebase with parallel agents,
  finds bugs using systematic debugging methodology, applies fixes with TDD,
  verifies with quality gates, builds knowledge graph, generates audit report.
  Includes: bug detection, security audit, performance check, accessibility scan,
  console cleanup, dead code removal, auto-fixing with verification.
  TRIGGER: user types /sam at start of message. Also trigger on "audit my project",
  "full code review", "scan all files", "project health check", "use /sam".
---

# /sam — Ultimate Project Audit Skill

Full-project scanner with parallel agents, systematic debugging, TDD fixes, verification gates. One command does everything.

---

## Step 0 — Activate Caveman Ultra Mode

All responses use caveman ultra after /sam runs:
- Drop articles, filler, pleasantries
- Abbreviate: DB/auth/config/req/res/fn/impl
- Arrows for causality: X → Y
- One word when one word enough
- Code blocks stay normal
- Security warnings = full sentences (safety exception)

---

## Step 1 — Parallel File Scanning

Dispatch parallel agents per independent domain:

```
Agent 1 → Scan src/ directory
Agent 2 → Scan tests/ directory  
Agent 3 → Scan config/ directory
Agent 4 → Scan assets/ directory
```

Each agent:
1. Finds all files in domain
2. Reads every file
3. Returns file list + initial observations

**When to parallelize:**
- 3+ independent directories
- No shared state between scans
- Different file types (JS, CSS, HTML, config)

**When sequential:**
- Small project (< 20 files)
- Tightly coupled files
- Need full context first

---

## Step 2 — Systematic Bug Detection

### Phase 1: Root Cause Investigation

For each bug found:

1. **Read error messages carefully**
   - Stack traces completely
   - Line numbers, file paths, error codes

2. **Reproduce consistently**
   - Exact steps to trigger
   - Every time or intermittent?

3. **Check recent changes**
   - Git diff, recent commits
   - New deps, config changes

4. **Trace data flow (deep errors)**
   - Where bad value originate?
   - What called this with bad value?
   - Trace up to find source

### Phase 2: Pattern Analysis

- Find similar working code in codebase
- Compare working vs broken
- List every difference
- Understand dependencies

### Phase 3: Hypothesis Formation

- State clearly: "X is root cause because Y"
- Test minimally: smallest possible change
- One variable at a time
- Verify before continuing

### Phase 4: Implementation

**Iron Law: NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST**

**Red flags → STOP and return to Phase 1:**
- "Quick fix for now, investigate later"
- "Just try changing X and see"
- "Add multiple changes, run tests"
- "Probably X, let me fix that"
- "One more fix attempt" (after 2+ failures)
- 3+ failed fixes = architectural problem, discuss with human

---

## Step 3 — TDD Fix Application

**Iron Law: NO PRODUCTION CODE WITHOUT FAILING TEST FIRST**

### Red-Green-Refactor for Every Fix

**RED** — Write failing test:
```typescript
test('rejects empty email', async () => {
  const result = await submitForm({ email: '' });
  expect(result.error).toBe('Email required');
});
```

**Verify RED** — Run test, confirm it fails correctly:
```bash
npm test
# FAIL: expected 'Email required', got undefined
```

**GREEN** — Minimal code to pass:
```typescript
if (!data.email?.trim()) {
  return { error: 'Email required' };
}
```

**Verify GREEN** — Run test, confirm passes:
```bash
npm test
# PASS
```

**REFACTOR** — Clean up, keep tests green

---

## Step 4 — Comprehensive Audit Checks

### 4.1 Bug Detection

| Check | What to look for |
|-------|-----------------|
| Syntax errors | broken brackets, unclosed tags, missing semicolons |
| Logic bugs | wrong conditions, off-by-one, `<` vs `<=` |
| Undefined vars | variables used before declaration |
| Null/undefined | missing null checks, optional chaining needed |
| Async issues | missing await, unhandled promises, race conditions |
| Console noise | `console.log`, `console.warn`, `console.error`, `debugger` |
| Dead code | unused imports, unreachable code, unused functions |
| Missing files | imports pointing to non-existent files |

### 4.2 Security Audit (40+ checks)

**Critical (full sentences, never caveman):**
- No API keys hardcoded
- No `innerHTML` without sanitization
- No `eval()` usage
- Parameterized queries only
- CORS properly configured
- Auth tokens in httpOnly cookies
- HTTPS enforcement
- Input validation on all boundaries
- CSP headers present
- No secrets in logs/errors

### 4.3 Structure Review

- File organization
- Import/export patterns
- Coupling between modules
- Circular dependencies

### 4.4 Performance Audit

- Asset sizes
- Memory leaks
- Bundle bloat
- Lazy loading opportunities
- Image optimization

### 4.5 Accessibility (WCAG 2.1 AA)

- ARIA labels
- Contrast ratios
- Keyboard navigation
- Alt text on images
- Form labels

### 4.6 Mobile/Responsive

- Viewport meta tag
- Breakpoint coverage
- Touch target sizes
- Responsive images

---

## Step 5 — Subagent-Driven Fix Implementation

For complex fixes or multiple files:

### Dispatch Pattern

1. **Implementer subagent** → Fixes bug with TDD
2. **Spec reviewer subagent** → Confirms code matches spec
3. **Code quality reviewer subagent** → Reviews implementation

### Model Selection

| Task Type | Model |
|-----------|-------|
| Mechanical (1-2 files, clear spec) | Fast/cheap |
| Integration (multi-file coordination) | Standard |
| Architecture/design/review | Most capable |

### Implementer Status Handling

| Status | Action |
|--------|--------|
| DONE | Proceed to spec review |
| DONE_WITH_CONCERNS | Read concerns, address if correctness issue |
| NEEDS_CONTEXT | Provide missing context, re-dispatch |
| BLOCKED | Assess: context? → re-dispatch; reasoning? → upgrade model; too large? → split task; plan wrong? → escalate to human |

**Never:**
- Skip spec compliance review before code quality review
- Accept "close enough" on spec compliance
- Move to next task with open review issues
- Dispatch multiple implementers in parallel

---

## Step 6 — Verification Before Completion

**Iron Law: NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE**

### The Gate Function

```
1. IDENTIFY: What command proves this claim?
2. RUN: Execute FULL command (fresh, complete)
3. READ: Full output, check exit code, count failures
4. VERIFY: Does output confirm claim?
   - NO: State actual status with evidence
   - YES: State claim WITH evidence
5. ONLY THEN: Make claim
```

### Required Verifications

| Claim | Requires |
|-------|----------|
| Tests pass | Test output: 0 failures |
| Linter clean | Linter output: 0 errors |
| Build succeeds | Build: exit 0 |
| Bug fixed | Original symptom test: passes |
| Security clean | Security scan: 0 critical issues |

**Red flags → STOP:**
- Using "should", "probably", "seems to"
- Expressing satisfaction before verification
- Trusting agent success reports
- "Just this once" thinking

---

## Step 7 — Build Project Knowledge Graph

Map project structure:

1. **God nodes** — files/modules everything depends on
2. **Clusters** — group related files by feature/domain
3. **Dependency edges** — who imports who
4. **Dead ends** — files with no imports and no dependents
5. **Design rationale** — read comments tagged `// NOTE:` `// WHY:` `// HACK:` `// TODO:`

Output:
```
GRAPH: api.js → auth, utils, components
Clusters: auth/, dashboard/, settings/
Dead ends: helpers.js, legacy.js
God nodes: config.js (imported by 12 files)
```

---

## Step 8 — Generate Audit Report

Create `SAM_AUDIT_REPORT.md` in project root.

### Report Structure

```markdown
# /sam Audit Report
Generated: [date]

## Executive Summary
- Files scanned: [N]
- Bugs found: [N] critical, [N] warnings
- Security issues: [N] critical, [N] warnings
- Console lines removed: [N]
- Dead code removed: [N] items
- Health score: [X]/10

## Project Structure Map
[folder tree + god nodes + clusters + dead ends]

## Bug Summary by Severity

### Critical
- [file]: [bug] | WHY: [cause] | FIX: [what was done]

### Warnings
- [file]: [issue] | WHY: [cause] | FIX: [what was done]

## Security Audit
[Full sentences for security issues]

## Performance Audit
[Asset sizes, memory leaks, bundle issues]

## Accessibility Audit
[WCAG compliance issues]

## Console Noise Removed
- [file]: line [N] - [type]

## Dead Code Removed
- [file]: [what was removed]

## Project Health Score
[X]/10 — [reason]

## What to Do Next
1. [highest priority]
2. [structural improvement]
3. [feature/refactor suggestion]
4. [testing suggestion]
5. [deployment/performance tip]

## Verification Evidence
- Tests: [command] → [result]
- Linter: [command] → [result]
- Build: [command] → [result]
```

---

## Step 9 — Production Gate (20-Point Checklist)

Before claiming SHIP IT:

1. All tests pass
2. No console.log/debugger left
3. No hardcoded secrets
4. Security scan clean
5. Linter clean
6. Type check passes
7. Build succeeds
8. No TODO/FIXME in code
9. Error handling present
10. Loading states present
11. Responsive design verified
12. Accessibility checked
13. Performance acceptable
14. No unused imports
15. No dead code
16. Documentation updated
17. CHANGELOG updated
18. Version bumped
19. Git commit clean
20. Human review approved

**SHIPT IT** only if all 20 pass.
**NOT YET** with specific failures if any fail.

---

## Step 10 — Human Score & CLAUDE.md Export

### Human Score (0-100)

Rate code quality with specific deductions:
- -10 per console.log left in production
- -10 per security vulnerability
- -5 per unused import
- -5 per missing error handling
- -5 per magic number
- -10 per missing test for critical path
- -5 per accessibility violation
- -10 per performance issue

### CLAUDE.md Generator

Export project memory:
- Project type and stack
- Architecture patterns
- Key files and their roles
- Gotchas and special cases
- Build/test commands

---

## Caveman Response Template

```
/sam complete. [X] files scanned. [N] bugs. [M] warnings. [K] console lines removed.

CRITICAL:
- [file]: [bug] → [fix applied]

SECURITY:
- [file]: [issue] → [fix applied]

WARNINGS:
- [file]: [issue] → [fix applied]

CONSOLE REMOVED: [N] lines across [M] files

GRAPH: [god node] → [cluster1], [cluster2]...
Dead ends: [file], [file]

HEALTH: [X]/10 — [reason]
HUMAN SCORE: [X]/100

NEXT:
1. [action]
2. [action]
...

Full report → SAM_AUDIT_REPORT.md
```

---

## Token Budget Rules

- Never repeat info already stated
- Use abbreviations in caveman mode
- One-line per bug in summary
- Full detail in SAM_AUDIT_REPORT.md only
- Graph summary = max 5 lines in chat

---

## Memory (Session-Persistent)

After first /sam run, remember:
- Project type (React/Node/vanilla JS/Python/etc)
- God nodes
- Recurring patterns (same bug in multiple files)
- What was already fixed this session
- Security issues found
- Performance bottlenecks

On follow-up questions, use graph knowledge — don't re-scan unless user says `/sam refresh`.

---

## Command

Only one command: `/sam`

Does everything — parallel scan, systematic debugging, TDD fixes, security audit, performance check, accessibility scan, verification gates, knowledge graph, report generation, human score, CLAUDE.md export.

No flags. No subcommands. Just `/sam`.
