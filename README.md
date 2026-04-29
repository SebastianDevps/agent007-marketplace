# Agent007 Marketplace

Official marketplace for Agent007 — autonomous AI development orchestration for Claude Code.

---

```
╔═══════════════════════════════════════════════════════════════════╗
║                                                                   ║
║   _  ___  ___ _  _  ____  ___  ___  _____                         ║
║  /_\/ __ | _ | \| ||_  _|/ _ \/ _ \| __ /                         ║
║ / _ \ (_ | _ | .` | | | | (_)| (_)| /  /                          ║
║/_/ \_\___|___|_|\_| |_|  \___/\___//_ /                           ║
║                                                                   ║
║  Autonomous AI Development Orchestration · v5.1.1                 ║
║  10 agents · 35 skills · 21 hooks · OpenClaw primitives           ║
║                                                                   ║
║  ▸ /dev "task"         → auto-classifies & routes                 ║
║  ▸ /consult "question" → expert consultation                      ║
║  ▸ /ralph-loop "task"  → autonomous loop until COMPLETE           ║
║  ▸ /orchestrate        → multi-agent workflow with HANDOFF        ║
║                                                                   ║
╚═══════════════════════════════════════════════════════════════════╝
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

### Updates

```bash
/plugin update agent007
```

---

## What You Get

### 3 Entry Commands

```bash
/dev "task"              # Auto-classifies complexity, selects workflow, executes autonomously
/consult "question"      # Routes to the right expert agent with skill injection
/orchestrate "workflow"  # Multi-agent chain with structured HANDOFF between agents
```

### 8 Expert Agents

| Agent | Tool Profile | Domain |
|-------|-------------|--------|
| `backend-db-expert` | coding | APIs, NestJS, TypeORM, databases, distributed systems |
| `security-expert` | minimal | OWASP, JWT, threat modeling, compliance |
| `frontend-ux-expert` | coding | React, Next.js, UX, accessibility, GSAP |
| `platform-expert` | coding | CI/CD, Docker, testing, quality gates |
| `product-expert` | minimal | Product discovery, roadmap, user stories |
| `code-reviewer` | minimal | CRITICAL/HIGH/MEDIUM/LOW taxonomy, 80% confidence filter |
| `loop-operator` | full | Ralph loop control, stall detection, Steer Pattern |
| `refactor-cleaner` | coding | Dead code removal via knip/depcheck/ts-prune |

### 28 Hooks — run automatically on every session

**Quality gates (always active):**
`sdd-guard` · `pre-commit-guard` · `block-no-verify` · `safety-guard` · `config-guard` · `format-on-save` · `context-window-guard`

**OpenClaw primitives (v5.1):**

| Hook | Trigger | What it does |
|------|---------|--------------|
| `tool-loop-detection` | PostToolUse/all | Circuit breaker at 30 identical calls |
| `context-engine` | PreToolUse/Agent | Token budget check before every spawn |
| `mutation-guard` | PreToolUse/Write\|Edit | Deduplicates writes by content hash |
| `memory-decay` | SessionStart | Archives stale memories (30/60 day decay) |
| `tool-policy-guard` | PreToolUse/Write\|Edit | Enforces minimal/coding/full per agent |
| `provider-rotation` | PreToolUse/Agent | Failover: opus → sonnet → haiku on cooldown |
| `transcript-policy` | SubagentStart | Injects model-tier directive per subagent |

### Autonomous Workflows

```
/dev "task"
 ├── Simple  → generate → verify → done
 ├── Medium  → plan → wave-execute subagents → code-review → branch options
 └── Complex → brainstorm → worktree → plan → wave-execute + ralph loop → human gate
```

**Yield Pattern** — tasks with no shared dependencies run in parallel (multiple Agent() calls in one response). Wave scheduler groups them automatically via topological sort.

**Steer Pattern** — when a subagent drifts (wrong direction, not stalled), loop-operator sends guidance via SendMessage before kill+restart. Preserves context and momentum.

---

## Platform

**macOS · Linux · Windows** — all hooks are Python 3 or Node.js, no bash dependencies.

---

## Honest Comparison

| Capability | Claude Code vanilla | Agent007 |
|---|:---:|:---:|
| Complexity-based routing (simple/medium/complex) | ❌ | ✅ `/dev` |
| Loop until verified complete | ❌ | ✅ Ralph |
| Specialized agents by domain | ❌ | ✅ 8 experts |
| Parallel subagent execution (Yield Pattern) | ❌ | ✅ |
| Mid-flight agent guidance (Steer Pattern) | ❌ | ✅ |
| Tool policy enforcement per agent | ❌ | ✅ 28 hooks |
| Token loop detection + circuit breaker | ❌ | ✅ |
| Memory temporal decay | ❌ | ✅ |

Token cost with Ralph active: 2–3× single-pass. Use it when an incomplete task costs more than extra tokens.

---

## Documentation

Full docs: https://github.com/SebastianDevps/agent007-doc  
Plugin source: https://github.com/SebastianDevps/agent007  
License: MIT · Author: Sebastian Guerra

---

**Version**: 5.1.1 · `10 agents` · `35 skills` · `21 hooks` · `OpenClaw primitives`
