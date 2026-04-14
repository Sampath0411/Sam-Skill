# /sam — Claude Code Skill

> Full project audit + bug scanner + knowledge graph + caveman mode. One command.

[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blue)](https://claude.ai/code)

---

## What it does

Type `/sam` in Claude Code and it will:

- 🔍 **Scan every file** in your project
- 🐛 **Find all bugs, errors, warnings** — and explain why each one exists
- 🔇 **Remove console noise** (console.log, console.warn, debugger)
- 🗺️ **Map your project** like a knowledge graph (god nodes, clusters, dead ends)
- 📋 **Generate `SAM_AUDIT_REPORT.md`** — full audit report in your project root
- ➡️ **Suggest what to do next** based on your actual code
- 🪨 **Responds in caveman mode** — ultra-compressed, saves tokens

---

## Install

```bash
mkdir -p ~/.claude/skills/sam
curl -fsSL https://raw.githubusercontent.com/Sampath0411/sam-skill/main/SKILL.md \
  > ~/.claude/skills/sam/SKILL.md
```

Add to `~/.claude/CLAUDE.md`:

```
- **sam** (`~/.claude/skills/sam/SKILL.md`) - full project audit. Trigger: /sam
When the user types /sam, invoke the Skill tool with `skill: "sam"` before doing anything else.
```

---

## Command

```
/sam
```

That's it. One command. Does everything — scan, fix, map, report, next steps.

---

## Example output

```
/sam complete. 34 files scanned. 7 bugs. 12 warnings. 23 console lines removed.

CRITICAL:
- auth.js: token expiry check use < not <= → fixed
- api.js: missing await on fetchUser() → race condition

WARNINGS:
- utils.js: unused import 'lodash' → removed
- index.html: missing alt on 3 images → flagged

CONSOLE REMOVED: 23 lines across 8 files

GRAPH: api.js → auth, utils, components
Dead ends: helpers.js, legacy.js

HEALTH: 6/10 — no error handling on async fns

NEXT:
1. Add try/catch to all async functions
2. Set up ESLint to catch this automatically
3. Move legacy.js to /archive or delete
4. Add loading states to all fetch calls
5. Write tests for auth module

Full report → SAM_AUDIT_REPORT.md
```

---

## Skills combined

This skill merges:
- **[caveman](https://github.com/Sampath0411/sam-skill)** — ultra-compressed token-efficient responses
- **[graphify](https://github.com/safishamsi/graphify)** — project knowledge graph & structure mapping
- **Custom audit layer** — bug detection, console cleanup, fix suggestions

---

## Made by

**Sampath** — [@Sampath0411](https://github.com/Sampath0411)

Built for Claude Code. `/sam` and go.
