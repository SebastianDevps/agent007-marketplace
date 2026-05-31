# Agent007 Marketplace — v7 Release

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
║  Autonomous AI Development Orchestration · v7.0.2                 ║
║  13 agents · 57 skills · 43 hooks · CI propia · 0 debt            ║
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

## What's new in v7

- **13 expert agents** — specialized routing per domain (backend, frontend, platform, security, product, observability, incident response). New: `docs-architect`, `error-coordinator`, `incident-responder`, `observability-engineer`, `architect-reviewer` for cross-module consistency validation.
- **57 skills** — flat registry (depth-1), all callable. New domain skills: `domain-behavioral-contracts` (DECLARE_BEFORE_ACT, SCOPE_IS_CONTRACT, SIMPLEST_SOLUTION, VERIFY_NOT_ASSUME), `dispatching-parallel-agents`, plus refined SDD gates (sdd-analyze, sdd-checklist, sdd-debate, sdd-verify-diff).
- **43 deterministic hooks** — across 7 event channels. V7.3 hardening: atomic writes, concurrent file locks, idempotency deduping. New: `tool-policy-guard` (minimal/coding/full per agent), `context-engine` (token budget pre-dispatch), `transcript-policy` (model assignment per subagent tier).
- **SDD pipeline with 4 auto-gates** — proposal → spec (checklist-gate) → design (debate-gate) → tasks → apply → verify (diff-verify-gate) → archive. Each gate has explicit verdict (PASS/WARN/FAIL/blocked/findings/clean).
- **V7.3 auto-loop hardened** — fail-and-retry with structural feedback, convergence detection (2× identical failure signature → escalate), wall-clock watchdog (60 min), per-tier×per-trigger budget. Parallel fan-out with worktree isolation for multi-domain apply waves.
- **File-based state only** — no external backends. All SDD artifacts in `openspec/changes/<change>/`. Persistent feedback loop, cross-session recovery via `.sdlc/state/` directory.
- **Behavioral contracts as identity** — DECLARE_BEFORE_ACT, SCOPE_IS_CONTRACT, SIMPLEST_SOLUTION, VERIFY_NOT_ASSUME embedded in `domain-behavioral-contracts` skill and auto-injected.
- **First-run onboarding** — `/sdd-onboard` guided walkthrough using your real codebase (tech-stack detection, test-runner discovery, strict-TDD opt-in).
- **Tool allowlist + executor classification** — PreToolUse hooks block hallucinated paths, enforce skill-level bash whitelist (shadcn pattern), classify writes as read-only / read-mostly / read-write per agent policy. Safety guard hardened with pipe data-flow detection.

---

## What You Get

### 6 Entry Commands

```bash
/dev "task"              # Auto-classifies complexity, routes inline or SDD
/consult "question"      # Routes to the right expert agent with skill injection
/ralph-loop "task"       # Autonomous loop until verified COMPLETE
/orchestrate "workflow"  # Multi-agent chain with structured HANDOFF
/prompt-gen "objective"  # Convert vague intent into precision prompt
/security-scan          # OWASP + codebase audit
```

### 13 Expert Agents

| Agent | Domain |
|-------|--------|
| `backend-db-expert` | APIs, NestJS, TypeORM, databases, microservices, resilience patterns |
| `frontend-ux-expert` | React, Next.js, Tailwind, GSAP, shadcn, Spline, barba, iOS HIG, component builders |
| `security-expert` | OWASP, JWT, OAuth, threat modeling, compliance, encryption, auth |
| `platform-expert` | CI/CD, Docker, Jest, Playwright, Kubernetes, monitoring, infra |
| `product-expert` | RICE, user stories, roadmap, MVP, backlog prioritization |
| `code-reviewer` | Quality checks (CRITICAL/HIGH/MED/LOW), 80% confidence filter, diff review |
| `architect-reviewer` | Architecture review, design patterns, bounded contexts, module boundaries, technical debt |
| `docs-architect` | Technical writing, API docs, onboarding, system overviews, design system documentation |
| `incident-responder` | Outage response, P0/P1 triage, postmortems, runbooks, rollback strategies |
| `observability-engineer` | Monitoring, metrics, traces, Prometheus, Grafana, OpenTelemetry, SLO/SLI |
| `loop-operator` | Ralph loop control, stall detection, autonomous retries, steering patterns |
| `refactor-cleaner` | Dead code removal, depcheck, knip, ts-prune, import cleanup |
| `error-coordinator` | Cascading subagent failure recovery, retry orchestration, multi-agent error resolution |

### 57 Skills

Organized by category:

- **Pipeline** (16): plan, generate, verify, brainstorming, tdd-workflow, subagent-driven-development, using-git-worktrees, finishing-a-development-branch, sop-reverse, adr-review, adr-write, prd-author, retrospective, issue-creation, spec, receiving-code-review
- **Orchestration** (9): session-manager, ralph-loop-wrapper, iterative-retrieval, sdd-apply, sdd-debate, sdd-verify-diff, consult-decide, consult-critique, dispatching-parallel-agents
- **Domain** (18): domain-api-design-principles, domain-architecture-patterns, domain-resilience-patterns, domain-nestjs-code-reviewer, domain-security-review, domain-react-best-practices, domain-frontend-design, domain-gsap, domain-discovery-before-code, domain-shadcn-component-install, domain-a11y-contrast-check, domain-design-tokens-extract, domain-design-system-doc, domain-page-transitions-barba, domain-ios-hig-mobile, domain-spline-3d-embed, domain-behavioral-contracts
- **Quality Gates** (3): quality-gates-systematic-debugging, agent-self-diagnosis, quality-gates-performance-profiling
- **Devrel** (1): devrel-api-documentation
- **Product** (1): product-product-discovery
- **Workflow Utils** (7): commit, pull-request, changelog, deep-research, search-first, rules-distill, skill-stocktake
- **Meta** (1): writing-skills

### 43 Hooks — run automatically every session

**Auto-injected quality gates:**
`sdd-guard` · `pre-commit-guard` · `block-no-verify` · `safety-guard` · `config-guard` · `format-on-save` · `context-window-guard`

**Defensive + discovery guards:**
`path-existence-guard` · `tool-allowlist-guard` · `frontend-discovery-gate` · `context-tick` · `session-recover` · `mutation-guard` · `web-distill` · `tool-loop-detection` · `context-engine` · `memory-decay` · `tool-policy-guard` · `transcript-policy`

Additional specialized hooks across SDD phases, routing, CLI, and telemetry.

### Autonomous Workflows

```
/dev "task"
 ├── Trivial      → generate → verify → done
 └── Substantial  → SDD pipeline (proposal → spec → design → tasks → apply → verify → archive)
                    with 4 auto-gates (checklist, debate, analyze, diff-verify)
```

**Parallel fan-out** — independent domain tasks run concurrently with worktree isolation. **Wave scheduling** — tasks grouped by dependency tiers via topological sort. **Steer Pattern** — drifting subagents receive mid-flight guidance via SendMessage.

---

## SDD Pipeline

### The Phases (each creates an artifact)

1. **Proposal** — user intent, scope, rough approach
2. **Spec** → **Gate 1** (checklist): observable requirements, Given/When/Then scenarios
3. **Design** → **Gate 2** (debate): competing architectural approaches, rationale, decision record
4. **Tasks** → **Gate 3** (analyze): breakdown to 2-5min executable tasks with TDD steps, cross-artifact consistency check
5. **Apply** → parallel subagent execution, auto-loop on test failure
6. **Verify** → two-pass validation (evidence + spec compliance)
7. **Archive** → final report, close change, persist to `openspec/changes/`
8. **Optional Gate 4** (diff-verify): adversarial per-file review before archive

All artifacts live in `openspec/changes/<change-name>/` — committable, shareable, auditable.

---

## Platform

**macOS · Linux · Windows** — all hooks are Python 3, no bash dependencies. CI runs on `ubuntu-latest`.

---

## Honest Comparison

| Capability | Claude Code vanilla | Agent007 v7 |
|---|:---:|:---:|
| Complexity-based routing (trivial / substantial → SDD) | ❌ | ✅ `/dev` |
| Loop until verified complete | ❌ | ✅ Ralph |
| Specialized agents by domain (13 experts) | ❌ | ✅ |
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
| Behavioral contracts as identity | ❌ | ✅ 4 core contracts |
| First-run tech-stack detection + TDD discovery | ❌ | ✅ `/sdd-onboard` |
| SDD auto-gates (4 phases) | ❌ | ✅ checklist, debate, analyze, diff-verify |
| File-based state (no backends) | ❌ | ✅ openspec/ + .sdlc/ |

---

## Documentation

- Plugin source: https://github.com/SebastianDevps/agent007
- Author: Sebastian Guerra
- License: MIT

---

**Version**: 7.0.2 · `13 agents` · `57 skills` · `43 hooks` · `4 SDD auto-gates` · `0 eager-loaded violations` · `behavioral-contracts-as-identity`
