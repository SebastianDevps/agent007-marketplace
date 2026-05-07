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
║  Autonomous AI Development Orchestration · v6.0.0                 ║
║  8 agents · 44 skills · 26 hooks · CI propia · 0 debt             ║
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

## What's new in v6

- **Frontend agent ejecuta** — antes solo validaba. Ahora escribe código (Write/Edit/Bash + WebFetch). 4 modos explícitos: BUILDER (default) · PLANNER · CONSULTANT · REVIEWER (opt-in).
- **Anti-convergence inevitable** — `frontend-discovery-gate` (PreToolUse hook) bloquea writes en `.tsx/.jsx/.css/.html/.svelte/.vue/.astro` sin un discovery output reciente. No depende del LLM recordar — está en la herramienta.
- **8 skills nuevas accionables** — `discovery-before-code`, `shadcn-component-install`, `a11y-contrast-check` (script Node.js zero-deps WCAG), `design-tokens-extract`, `design-system-doc` (9-section schema), `page-transitions-barba`, `ios-hig-mobile`, `spline-3d-embed`.
- **CI propia + debt register vacío** — 6-job GitHub workflow valida settings.json, frontmatter, hook syntax, line caps, references resolvable. `.line-cap-exemptions` está vacío: cero archivos eager > 200 líneas.
- **Eager-loaded total reducido 84%** (~7300 → 1195 líneas). Auto-inject overhead reducido 81% (1239 → 237 líneas por sesión).
- **Telemetría persistente + cross-session recovery** — `context-tick.py` (SessionStart + PostToolUse + Stop) escribe a `.sdlc/state/context-budget.jsonl`. `session-recover.py` lee tail al arrancar, emite resumen de sesión previa si <4h. `waste-report.py` audit: top files, hit rate, p95 tokens, never-loaded references.
- **Lifecycle scripts** — `verify.sh`, `install.sh`, `uninstall.sh`, `sync-to-public.sh`, `test-hooks.py` (13 fixtures regression), `waste-report.py`.

---

## What You Get

### 3 Entry Commands

```bash
/dev "task"              # Auto-classifies complexity, routes inline or SDD
/consult "question"      # Routes to the right expert agent with skill injection
/orchestrate "workflow"  # Multi-agent chain with structured HANDOFF
```

### 8 Expert Agents

| Agent | Tool Profile | Domain |
|-------|-------------|--------|
| `backend-db-expert` | coding | APIs, NestJS, TypeORM, databases, microservices |
| `frontend-ux-expert` ⚡ | coding | **BUILDER** mode default — writes code, not reviews. React, Next.js, Tailwind, GSAP, shadcn, Spline, barba, iOS HIG. Anti-convergence gate enforced. |
| `security-expert` | minimal | OWASP, JWT, threat modeling, compliance |
| `platform-expert` | coding | CI/CD, Docker, Jest, Playwright, Kubernetes, monitoring |
| `product-expert` | minimal | RICE/ICE, user stories, roadmap, AARRR |
| `code-reviewer` | minimal | CRITICAL/HIGH/MED/LOW taxonomy, 80% confidence filter |
| `loop-operator` | full | Ralph loop control, stall detection, Steer Pattern |
| `refactor-cleaner` | coding | Dead code via knip/depcheck/ts-prune |

> Removed in v6: `architect` → use `Skill('architecture-patterns')`. `performance-optimizer` → use `Skill('performance-profiling')` (now a skill with 3 layer-specific protocol references).

### 44 Skills

Organized by category, all with frontmatter contracts (`allowed-tools`, `canonical-sources`, `references`, `when.keywords`):

- **core/** (auto-inject): `quality-enforcement`, `banned-phrases`, `context-awareness`
- **pipeline/**: `plan`, `generate`, `verify`, `tdd-workflow`, `subagent-driven-development`, `using-git-worktrees`, `finishing-a-development-branch`, `sop-reverse`, `brainstorming`
- **orchestration/** (auto-inject): `session-manager`, `state-sync`, `iterative-retrieval`, `ralph-loop-wrapper`
- **domain/**: `api-design-principles`, `architecture-patterns`, `resilience-patterns`, `nestjs-code-reviewer`, `security-review`, `react-best-practices`, `frontend-design`, `gsap`, `karpathy`, plus the 8 new frontend executors
- **quality-gates/**: `systematic-debugging`, `agent-self-diagnosis`, `performance-profiling`
- **workflow-utils/**: `commit`, `pull-request`, `changelog`, `deep-research`, `search-first`, `rules-distill`, `skill-stocktake`
- **product/**, **devrel/**, **issue-creation/**: domain-specific entry points

### 26 Hooks — run automatically every session

**Quality gates (always active):**
`sdd-guard` · `pre-commit-guard` · `block-no-verify` · `safety-guard` · `config-guard` · `format-on-save` · `context-window-guard`

**Defensive guards:**

| Hook | Trigger | What it does |
|------|---------|--------------|
| `path-existence-guard` ⭐ | PreToolUse/Edit\|Write\|Read | Blocks hallucinated paths |
| `tool-allowlist-guard` ⭐ | PreToolUse/Bash | Skill-level bash whitelist (shadcn pattern) |
| `frontend-discovery-gate` ⭐ | PreToolUse/Edit\|Write | Blocks visual writes without recent discovery output (TTL 30 min) |
| `context-tick` ⭐ | SessionStart + PostToolUse + Stop | Persists telemetry to `.sdlc/state/context-budget.jsonl` |
| `session-recover` ⭐ | SessionStart | Emits previous-session preamble if last activity <4h ago |
| `mutation-guard` | PreToolUse/Write\|Edit | Deduplicates writes — defensive against bug retries |
| `web-distill` | PreToolUse/WebFetch | Distills HTML + 24h URL cache |
| `tool-loop-detection` | PostToolUse/all | Circuit breaker at 30 identical calls |
| `context-engine` | PreToolUse/Agent | Token budget check before every spawn |
| `memory-decay` | SessionStart | Archives stale memories (30/60 day) |
| `tool-policy-guard` | PreToolUse/Write\|Edit | Enforces minimal/coding/full per agent |
| `transcript-policy` | SubagentStart | Injects model-tier directive per subagent |

⭐ = new in v6.

### Lifecycle scripts

```bash
.claude/scripts/lifecycle/verify.sh                   # 5 checks (+ optional 6th: hook regression tests)
.claude/scripts/lifecycle/test-hooks.py               # 13 fixture-based regression tests
.claude/scripts/lifecycle/waste-report.py             # telemetry audit: top files, hit rate, p95
.claude/scripts/lifecycle/install.sh /path/to/proj    # deploy to a project
.claude/scripts/lifecycle/uninstall.sh /path/to/proj  # remove (preserves state)
```

CI gate (`.github/workflows/plugin-validate.yml`) runs the same 5 checks on every PR.

### Autonomous Workflows

```
/dev "task"
 ├── Trivial      → generate → verify → done
 └── Substantial  → SDD pipeline (proposal → spec → design → tasks → apply → verify → archive)
```

**Yield Pattern** — independent tasks run in parallel (multiple `Agent()` calls per response). Wave scheduler groups via topological sort.

**Steer Pattern** — drifting subagents get mid-flight guidance via SendMessage before kill+restart.

---

## Frontend executor (new in v6)

Antes el agente solo validaba — sus tools eran `[Read, Grep, Glob]`. Ahora es **builder**:

```
.claude/state/discovery-output.json
 ↑ written by Skill('discovery-before-code')
 ↓ read by frontend-discovery-gate hook (PreToolUse/Edit|Write)

If output missing or > 30 min old → write to .tsx/.css is BLOCKED.
```

The skill enforces 4 steps before any code:
1. **Referent fetch** — real URL, not "modern dashboard"
2. **Pick 1 of 11 extreme styles** (brutalist / cyberpunk / swiss / memphis / etc.) — anti-convergence
3. **States table** (empty / loading / error / success / edge)
4. **Tokens declared** (≤5 colors, ≤2 fonts)

Then the executable skills take over: `shadcn-component-install`, `design-tokens-extract`, `a11y-contrast-check`, `page-transitions-barba`, `ios-hig-mobile`, `spline-3d-embed`, `design-system-doc`.

---

## Platform

**macOS · Linux · Windows** — all hooks are Python 3, no bash dependencies. CI runs on `ubuntu-latest`.

---

## Honest Comparison

| Capability | Claude Code vanilla | Agent007 v6 |
|---|:---:|:---:|
| Complexity-based routing (trivial / substantial → SDD) | ❌ | ✅ `/dev` |
| Loop until verified complete | ❌ | ✅ Ralph |
| Specialized agents by domain | ❌ | ✅ 8 experts |
| Parallel subagent execution (Yield Pattern) | ❌ | ✅ |
| Mid-flight agent guidance (Steer Pattern) | ❌ | ✅ |
| Tool policy + bash allowlist per skill | ❌ | ✅ shadcn pattern |
| Hallucinated path block | ❌ | ✅ `path-existence-guard` |
| Anti-convergence enforcement (frontend) | ❌ | ✅ `frontend-discovery-gate` |
| Token loop detection + circuit breaker | ❌ | ✅ |
| Memory temporal decay | ❌ | ✅ |
| Plugin self-CI (frontmatter, line caps, refs) | ❌ | ✅ 6-job workflow |
| Hook regression tests | ❌ | ✅ 13 fixtures |
| Persistent telemetry + waste audit | ❌ | ✅ `context-tick` + `waste-report.py` |
| Cross-session recovery (no PreCompact native) | ❌ | ✅ `session-recover` |
| Debt register (explicit, validated) | ❌ | ✅ `.line-cap-exemptions` (currently empty) |

---

## Documentation

- Plugin source: https://github.com/SebastianDevps/agent007
- Author: Sebastian Guerra
- License: MIT

---

**Version**: 6.0.0 · `8 agents` · `44 skills` · `26 hooks` · `72 lazy-load references` · `0 eager-loaded violations` · `13 hook regression tests`
