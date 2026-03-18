# Agent007 Marketplace

Official marketplace for Agent007 — autonomous AI development orchestration for Claude Code CLI.

---

```
╔════════════════════════════════════════════════════════════════════╗
║                                                                    ║
║   _  ___  ___ _  _  ____  ___  ___  _____                          ║
║  /_\/ __ | _ | \| ||_  _|/ _ \/ _ \| __ /                          ║
║ / _ \ (_ | _ | .` | | | | (_)| (_)| /  /                           ║
║/_/ \_\___|___|_|\_| |_|  \___/\___//_ /                            ║
║                                                                    ║
║  Autonomous AI Development Team · v4.1 · by Sebastian Guerra       ║
║  5 agents · 41 skills · 16 commands                                ║
║                                                                    ║
║  ▸ /dev "task"         → auto-classifies & routes                  ║
║  ▸ /consult "question" → expert consultation                       ║
║  ▸ /ralph-loop "task"  → autonomous loop until COMPLETE            ║
║  ▸ /prompt-gen         → convert /consult output to /dev prompt    ║
║                                                                    ║
╚════════════════════════════════════════════════════════════════════╝
```

## Installation

### Step 1: Add the Marketplace

```bash
/plugin marketplace add SebastianDevps/agent007-marketplace
```

### Step 2: Install Agent007

```bash
/plugin install agent007@agent007-marketplace
```

**Done!** On first session, Agent007 shows a welcome banner in your terminal. From there, all commands are available.

### Updates

```bash
/plugin update agent007
```

---

## What You Get

### 4 Master Commands

```bash
/dev "task"              # Auto-classifies complexity, selects workflow, executes autonomously
/consult "question"      # Routes to the right expert agent with skill injection
/ralph-loop "task"       # Autonomous loop — iterates until task is verifiably complete
/prompt-gen "objective"  # Converts /consult output into a structured executable prompt
```

### 5 Expert Agents

| Agent | Model | Domain |
|-------|-------|--------|
| `backend-db-expert` | Opus | APIs, NestJS, TypeORM, databases, distributed systems |
| `security-expert` | Opus | OWASP, JWT, threat modeling, GDPR, SOC2 |
| `frontend-ux-expert` | Sonnet | React, Next.js, UX, accessibility, design systems |
| `platform-expert` | Sonnet | CI/CD, Docker, testing, quality gates |
| `product-expert` | Opus | Product discovery, roadmap, user stories |

### 41 Skills — auto-injected by context

Grouped by domain: `api-design-principles` · `architecture-patterns` · `resilience-patterns` · `security-review` · `nestjs-code-reviewer` · `react-best-practices` · `frontend-design` · `scenario-driven-development` · `systematic-debugging` · `verification-before-completion` · `writing-plans` · `subagent-driven-development` · `deep-research` · `commit` · `pull-request` · `changelog` · and 25 more.

### Autonomous Workflows

```
/dev "task"
 ├── Simple  → implement → verify → done
 ├── Medium  → plan → subagents per task → review → branch options
 └── Complex → brainstorm → worktree → plan → subagents + ralph loop
```

### Ralph Loop — iterate until complete

Claude's natural behavior is to stop when it thinks it's done. Ralph intercepts the Stop hook, checks for `<promise>COMPLETE</promise>`, and re-injects continuation context until all success criteria are met.

```bash
/ralph-loop "Build kanban board with Next.js + Tailwind"
# Requirements: localStorage, Todo/In Progress/Done columns, full CRUD
# Success: npm run build → 0 errors, npm run lint → 0 warnings
# Output <promise>COMPLETE</promise> when done.
--max-iterations 30
```

---

## Platform

**macOS · Linux · Windows** — all hooks are Python 3 or Node.js, no bash dependencies.

---

## Honest Comparison

| Capability | Claude Code vanilla | Agent007 |
|---|:---:|:---:|
| Complexity-based routing (simple/medium/complex) | ❌ | ✅ `/dev` |
| Loop until verified complete | ❌ | ✅ Ralph |
| Specialized agents by domain | ❌ | ✅ 5 experts |
| Skill injection on queries | ❌ | ✅ `/consult` |
| SDD enforcement (gate, not suggestion) | ❌ | ✅ hook |
| Subagents with clean context per task | ❌ | ✅ |

Token cost with Ralph active: 2-3x single-pass. Use it when incomplete tasks cost more than extra tokens.

---

## Documentation

- **GitHub**: https://github.com/SebastianDevps/agent007
- **License**: MIT
- **Author**: Sebastian Guerra

---

**Version**: 4.1.0 | `41 skills` · `5 agents` · `16 commands`
