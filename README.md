# /sam — Ultimate Claude Code Skill

> Full-project audit + systematic debugging + TDD fixes + parallel agents + verification gates + knowledge graph. The complete package.

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blue)](https://claude.ai/code)

---

## What it does

Type `/sam` in Claude Code and it will:

- 🔍 **Parallel file scanning** — Multiple agents scan different parts simultaneously
- 🐛 **Systematic bug detection** — Root cause investigation, not symptom fixes
- 🧪 **TDD fix application** — Every fix has a failing test first
- 🔒 **Security audit** — 40+ checks for vulnerabilities
- ⚡ **Performance audit** — Asset sizes, memory leaks, bundle bloat
- ♿ **Accessibility scan** — WCAG 2.1 AA compliance
- 🔇 **Console noise removal** — Auto-removes console.log/debugger
- 💀 **Dead code elimination** — Unused imports, unreachable code
- 🗺️ **Knowledge graph** — Maps god nodes, clusters, dead ends
- ✅ **Verification gates** — No completion claims without evidence
- 📋 **SAM_AUDIT_REPORT.md** — Full audit report
- 🎯 **Human score** — 0-100 rating with specific deductions
- 🧠 **CLAUDE.md export** — Project memory for future context
- 🪨 **Caveman mode** — Ultra-compressed responses save tokens

---

## Install

```bash
mkdir -p ~/.claude/skills/sam
curl -fsSL https://raw.githubusercontent.com/Sampath0411/Sam-Skill/main/SKILL.md \
  > ~/.claude/skills/sam/SKILL.md
```

Add to `~/.claude/CLAUDE.md`:

```
- **sam** (`~/.claude/skills/sam/SKILL.md`) - Full project audit. Trigger: /sam
When the user types /sam, invoke the Skill tool with `skill: "sam"` before doing anything else.
```

---

## Command

```
/sam
```

That's it. One command. Does everything.

---

## Example output

```
/sam complete. 156 files scanned. 12 bugs. 23 warnings. 47 console lines removed.

CRITICAL:
- auth.js: token expiry check use < not <= → fixed with TDD
- api.js: missing await on fetchUser() → race condition fixed
- db.js: SQL injection risk → parameterized queries added

SECURITY:
- config.js: hardcoded API key → moved to env vars
- index.html: inline script → CSP nonce added

WARNINGS:
- utils.js: unused import 'lodash' → removed
- index.html: missing alt on 5 images → flagged

CONSOLE REMOVED: 47 lines across 12 files

GRAPH: api.js → auth, utils, components
Clusters: auth/, dashboard/, settings/
Dead ends: helpers.js, legacy.js

HEALTH: 8/10 — good structure, needs error handling
HUMAN SCORE: 78/100 (-10 security, -5 unused imports, -7 missing tests)

NEXT:
1. Add try/catch to all async functions
2. Set up ESLint for automatic catches
3. Write tests for auth module
4. Archive legacy.js
5. Add loading states to fetch calls

Full report → SAM_AUDIT_REPORT.md
```

---

## The 11 Phases

| Phase | What happens |
|-------|--------------|
| 0 | Caveman mode activation |
| 1 | Parallel file scanning |
| 2 | Systematic bug detection (4-phase root cause analysis) |
| 3 | TDD fix application (red-green-refactor) |
| 4 | Bug detection (syntax, logic, async, console, dead code) |
| 5 | Security audit (40+ checks) |
| 6 | Structure review |
| 7 | Performance audit |
| 8 | Accessibility scan |
| 9 | Verification gates (20-point checklist) |
| 10 | Knowledge graph generation |
| 11 | Report generation + human score + CLAUDE.md export |

---

## Iron Laws

**NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST**

**NO PRODUCTION CODE WITHOUT FAILING TEST FIRST**

**NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE**

---

## Skills merged

This skill combines:

- **systematic-debugging** — 4-phase root cause methodology
- **test-driven-development** — Red-green-refactor for every fix
- **verification-before-completion** — Evidence before assertions
- **dispatching-parallel-agents** — Parallel scanning for large projects
- **subagent-driven-development** — Multi-agent workflow for complex fixes
- **codepatch** — Security audit, performance check, human score

---

## Made by

**Sampath** — [@Sampath0411](https://github.com/Sampath0411)

Built for Claude Code. `/sam` and go.
