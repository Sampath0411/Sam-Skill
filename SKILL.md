---
name: sam
description: >
  Full-project audit skill. Scans every file in the codebase, finds bugs, errors, warnings,
  and console issues, explains why each problem exists, shows what was fixed, builds a knowledge
  graph of the project structure, suggests next steps, and outputs a complete audit report.
  Responds in ultra-compressed caveman mode to save tokens.
  TRIGGER: user types /sam at the start of a message. Also trigger when user says
  "audit my project", "check my code for bugs", "full code review", "scan all files",
  "project health check", or "use /sam". Always use this skill for any full-project
  code analysis request — even if not explicitly typed as /sam.
---

# /sam — Full Project Audit Skill

Caveman-mode full project scanner. Find bug. Fix bug. Map project. Tell what do next. Use few token.

---

## Step 0 — Activate Caveman Mode

All responses use **caveman ultra** for this entire session after /sam runs.

Rules:
- Drop articles, filler, pleasantries
- Fragments OK
- Abbreviate: DB/auth/config/req/res/fn/impl
- Arrows for causality: X → Y
- One word when one word enough
- Code blocks stay normal
- Security warnings stay full sentences (safety exception)

---

## Step 1 — Scan All Files

```
find . -type f \
  -not -path "*/node_modules/*" \
  -not -path "*/.git/*" \
  -not -path "*/dist/*" \
  -not -path "*/build/*" \
  -not -path "*/vendor/*" \
  -not -path "*/.next/*" \
  -not -path "*/coverage/*"
```

Read every file. No skip. Even small ones.

---

## Step 2 — Bug & Error Detection

For each file check:

| Check | What to look for |
|-------|-----------------|
| **Syntax errors** | broken brackets, unclosed tags, missing semicolons |
| **Logic bugs** | wrong conditions, off-by-one, bad comparisons (`<` vs `<=`) |
| **Undefined vars** | variables used before declaration |
| **Null/undefined** | missing null checks, optional chaining needed |
| **Async issues** | missing await, unhandled promises, race conditions |
| **Console noise** | `console.log`, `console.warn`, `console.error`, `debugger` left in code |
| **Dead code** | unused imports, unreachable code, unused functions |
| **Security** | hardcoded secrets, exposed API keys, `eval()`, XSS sinks |
| **CSS/HTML** | broken class refs, missing alt tags, invalid nesting |
| **Missing files** | imports pointing to non-existent files |

---

## Step 3 — Build Project Knowledge Graph (graphify-style)

Map the project structure like a knowledge graph:

1. **God nodes** — files/modules everything depends on
2. **Clusters** — group related files by feature/domain
3. **Dependency edges** — who imports who
4. **Dead ends** — files with no imports and no dependents
5. **Design rationale** — read comments tagged `// NOTE:` `// WHY:` `// HACK:` `// TODO:`

Output structure map in report. No need for actual graphify install — do it manually via file analysis.

---

## Step 4 — Generate Audit Report

Create file: `SAM_AUDIT_REPORT.md` in project root.

### Report structure:

```
# /sam Audit Report
Generated: [date]

## Project Structure Map
[folder tree + god nodes + clusters]

## Bug Summary
[count by severity]

## Bugs & Errors (file by file)
### [filename]
- ❌ BUG: [what] | WHY: [cause] | FIX: [what Claude did]
- ⚠️ WARN: [what] | WHY: [cause] | FIX: [what Claude did]
- 🔇 CONSOLE: [line] removed
- 💀 DEAD CODE: [what] removed

## Console Noise Removed
[list all console.log/warn/error removed with line numbers]

## Security Issues
[if any — full sentences, not caveman]

## Project Health Score
[X/10] — [one line reason]

## What to Do Next
1. [highest priority action]
2. [next action]
3. [next action]
...
```

---

## Step 5 — Apply Fixes

Auto-apply all safe fixes:
- Remove all `console.log`, `console.warn`, `console.error`, `debugger`
- Fix syntax errors
- Add null checks where needed
- Fix broken imports
- Remove unused imports

Tell user what changed, file by file.

---

## Step 6 — Suggest Next Steps

End every /sam run with:

```
## NEXT STEPS
1. [most critical fix if not auto-fixed]
2. [structural improvement]
3. [feature/refactor suggestion based on code]
4. [testing suggestion]
5. [deployment/performance tip if relevant]
```

Keep suggestions based on actual code found. No generic advice.

---

## Caveman Response Template

After scan completes, respond like:

```
/sam complete. [X] files scanned. [N] bugs. [M] warnings. [K] console lines removed.

CRITICAL:
- [file]: [bug] → [fix]

WARNINGS:
- [file]: [issue] → [fix]

CONSOLE REMOVED: [N] lines across [M] files

GRAPH: [god node] → [cluster1], [cluster2]...
Dead ends: [file], [file]

HEALTH: [X]/10 — [reason]

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
- One-line per bug in summary, full detail in report file
- Graph summary = max 5 lines in chat response
- Full data goes in SAM_AUDIT_REPORT.md

---

## Memory (session-persistent)

After first /sam run, remember:
- Project type (React/Node/vanilla JS/Python/etc)
- God nodes
- Recurring patterns (same bug in multiple files)
- What was already fixed this session

On follow-up questions, use graph knowledge — don't re-scan unless user says `/sam refresh`.

---

## Command

Only one command: `/sam`

Does everything — scan, find bugs, map project, remove console noise, generate report, suggest next steps. No flags. No subcommands. Just `/sam`.
