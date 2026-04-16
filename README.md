# /sam — Ultimate Claude Code Skill

> Full-project audit + systematic debugging + TDD fixes + parallel agents + verification gates + knowledge graph + webapp testing + research scout + memory consolidation + code review integration. The complete package.

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blue)](https://claude.ai/code)

---

## What it does

Type `/sam` in Claude Code and it will:

- 🔀 **Git worktree setup** — Isolated workspace for safe fix testing
- 🔍 **Parallel file scanning** — Multiple agents scan different parts simultaneously
- 🐛 **Systematic bug detection** — Root cause investigation, not symptom fixes
- 🔎 **Research scout** — Hunts web/Reddit/HN for unknown bug solutions
- 🧪 **TDD fix application** — Every fix has a failing test first
- 👥 **Subagent-driven fixes** — Multi-agent workflow for complex bugs
- 🔒 **Security audit** — 40+ checks for vulnerabilities
- ⚡ **Performance audit** — Asset sizes, memory leaks, bundle bloat
- ♿ **Accessibility scan** — WCAG 2.1 AA compliance
- 🔇 **Console noise removal** — Auto-removes console.log/debugger
- 💀 **Dead code elimination** — Unused imports, unreachable code
- 🗺️ **Graphify integration** — Deep knowledge graph with communities
- 🧠 **Memory consolidation** — Persists audit state across sessions
- 👁️ **Code review integration** — Request and receive reviews
- 🌐 **Webapp testing** — Playwright verification for web apps
- 📋 **SAM_AUDIT_REPORT.md** — Full audit report
- 🎯 **Human score** — 0-100 rating with specific deductions
- 🧩 **Finishing workflow** — Merge, PR, or cleanup options
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

## How It Works

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         /sam WORKFLOW                                    │
└─────────────────────────────────────────────────────────────────────────┘

User types /sam
       │
       ▼
┌─────────────────────┐
│ 0. Caveman Mode     │ ◄── Ultra-compressed responses
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ 1. Git Worktree     │ ◄── Isolated workspace for safe fixes
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ 2. Parallel Scan    │ ◄── Multiple agents scan directories
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐     ┌─────────────────────┐
│ 3. Bug Detection    │ ◄──►│ 4. Research Scout   │
│    (Systematic)     │     │    (if unknown)      │
└──────────┬──────────┘     └─────────────────────┘
           │
           ▼
┌─────────────────────┐     ┌─────────────────────┐
│ 5. TDD Fixes        │ ◄──►│ 6. Subagent Fixes   │
│    (Red-Green-Ref)  │     │    (complex bugs)    │
└──────────┬──────────┘     └─────────────────────┘
           │
           ▼
┌─────────────────────┐
│ 7. Audit Suite      │ ◄── Bug + Security + Performance + A11y
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ 8. Webapp Testing   │ ◄── Playwright (if applicable)
│ 9. Code Review      │ ◄── Request/receive reviews
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ 10. Verify Gates    │ ◄── 20-point checklist
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ 11. Graphify        │ ◄── Knowledge graph with communities
│ 12. Memory          │ ◄── Persist audit state
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ 13. Report          │ ◄── SAM_AUDIT_REPORT.md
│ 14. Production Gate │ ◄── SHIP IT or NOT YET
│ 15. Finish          │ ◄── Merge / PR / Keep / Discard
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   OUTPUT: Summary   │
│   + Full Report     │
│   + Worktree Path   │
└─────────────────────┘
```

### The Three Iron Laws

1. **NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST**
2. **NO PRODUCTION CODE WITHOUT FAILING TEST FIRST**
3. **NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE**

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
Surprising: utils.js connects auth and DB layers

HEALTH: 8/10 — good structure, needs error handling
HUMAN SCORE: 78/100 (-10 security, -5 unused imports, -7 missing tests)

NEXT:
1. Add try/catch to all async functions
2. Set up ESLint for automatic catches
3. Write tests for auth module
4. Archive legacy.js
5. Add loading states to fetch calls

Full report → SAM_AUDIT_REPORT.md
Worktree → .worktrees/sam-audit
```

---

## The 15 Steps

| Step | What happens |
|------|--------------|
| 0 | Caveman mode activation |
| 1 | Git worktree setup (isolation) |
| 2 | Parallel file scanning |
| 3 | Systematic debugging (4-phase root cause) |
| 4 | Research scout (web/Reddit/HN) |
| 5 | TDD fix application (red-green-refactor) |
| 6 | Subagent-driven fixes |
| 7 | Comprehensive audit (bug/security/perf/a11y) |
| 8 | Webapp testing (Playwright) |
| 9 | Code review integration |
| 10 | Verification gates (20-point checklist) |
| 11 | Graphify integration (deep knowledge graph) |
| 12 | Memory consolidation |
| 13 | Report generation + human score |
| 14 | Production gate |
| 15 | Finishing workflow (merge/PR/cleanup) |

---

## Iron Laws

**NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST**

**NO PRODUCTION CODE WITHOUT FAILING TEST FIRST**

**NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE**

---

## Skills merged (16 total)

This skill combines:

- **caveman-claude-skill** — Ultra-compressed token-efficient responses
- **systematic-debugging** — 4-phase root cause methodology
- **test-driven-development** — Red-green-refactor for every fix
- **verification-before-completion** — Evidence before assertions
- **dispatching-parallel-agents** — Parallel scanning for large projects
- **subagent-driven-development** — Multi-agent workflow for complex fixes
- **codepatch** — Security audit, performance check, human score
- **using-git-worktrees** — Isolated workspace for safe fix testing
- **consolidate-memory** — Session memory persists across audits
- **finishing-a-development-branch** — Cleanup, PR creation after audit
- **requesting-code-review** — Get review before claiming done
- **receiving-code-review** — Handle review feedback
- **executing-plans** — Multi-session execution for huge projects
- **graphify** — Deep knowledge graph with communities
- **research-scout** — Research unknown bug solutions
- **webapp-testing** — Live browser testing after fixes

---

## Made by

**Sampath** — [@Sampath0411](https://github.com/Sampath0411)

Built for Claude Code. `/sam` and go.
