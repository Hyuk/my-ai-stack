# My AI Stack

English | [한국어](README_KO.md)

My actual AI-powered development environment. This is how I build software in 2025 — not just writing code, but orchestrating AI agents to ship faster and better.

## Core: Claude Code + oh-my-claudecode

[Claude Code](https://claude.ai/code) is my primary AI coding assistant (CLI).
On top of it, I run [oh-my-claudecode (OMC)](https://github.com/anthropics/oh-my-claudecode) — a multi-agent orchestration layer that turns Claude Code into a full development platform.

### Why Claude Code?

- Terminal-native — works where I already work
- Agent mode with autonomous multi-step execution
- MCP (Model Context Protocol) support for extending capabilities
- Persistent conversation context across sessions

### oh-my-claudecode (OMC) v4.9.3

OMC adds a delegation-first architecture on top of Claude Code:

```
User Request
    │
    ▼
┌─────────────────┐
│   Orchestrator   │  ← Routes tasks to specialized agents
│  (Claude Opus)   │
└────────┬────────┘
         │
    ┌────┼────┬────────┬──────────┐
    ▼    ▼    ▼        ▼          ▼
 Explore Executor Designer Architect Researcher
 (Haiku) (Sonnet)  (Sonnet)  (Opus)   (Sonnet)
```

**32 Specialized Agents** across 3 model tiers:

| Tier | Model | Use Case | Agents |
|------|-------|----------|--------|
| LOW | Haiku | Quick lookups, simple edits | `explore`, `executor-low`, `architect-low`, `writer` |
| MEDIUM | Sonnet | Standard implementation, UI, testing | `executor`, `designer`, `researcher`, `qa-tester` |
| HIGH | Opus | Architecture, deep debugging, security | `architect`, `planner`, `critic`, `security-reviewer` |

**Key Execution Modes:**

| Mode | Description |
|------|-------------|
| **Autopilot** | Full autonomous execution from idea to working code |
| **Ultrawork** | Maximum parallel execution with multiple agents |
| **Ralph** | Persistence loop — keeps going until verified complete |
| **Team** | N coordinated agents on shared task list |
| **Pipeline** | Sequential agent chaining (e.g., explore → architect → executor) |

## MCP Servers

Model Context Protocol servers extend Claude Code's capabilities:

| Server | Purpose |
|--------|---------|
| **Context7** | Real-time library/framework documentation lookup |
| **Framer** | Design tool integration — CMS, pages, code files |
| **Gmail** | Email integration |
| **Google Calendar** | Calendar integration |

## gstack Skills (30+)

Production-grade workflows built on top of Claude Code:

| Category | Skills | What They Do |
|----------|--------|-------------|
| **QA & Testing** | `/qa`, `/qa-only`, `/browse` | Headless browser QA, bug detection, visual testing |
| **Code Review** | `/review`, `/plan-eng-review` | Pre-landing diff review, architecture review |
| **Shipping** | `/ship`, `/land-and-deploy` | PR creation, CI/CD, deploy verification |
| **Planning** | `/plan-ceo-review`, `/plan-eng-review`, `/plan-design-review` | Multi-perspective plan review (CEO, Eng, Design) |
| **Design** | `/design-consultation`, `/design-review` | Design system creation, visual QA |
| **Security** | `/cso` | OWASP Top 10, STRIDE threat modeling, dependency audit |
| **Monitoring** | `/canary`, `/benchmark` | Post-deploy canary checks, performance regression |
| **Documentation** | `/document-release`, `/retro` | Release docs, weekly retrospective |

## Other AI Tools

| Tool | Role | When I Use It |
|------|------|--------------|
| **OpenAI Codex CLI + OMX** | Independent second opinion | Cross-model code review, adversarial plan challenge. OMX (Oh My codeX) adds multi-agent orchestration to Codex |
| **Antigravity** | AI-powered development environment | Collaborative AI coding with visual context |
| **Cursor** | Visual AI code editor | When I need visual diff/context alongside AI |
| **VS Code** | Traditional IDE | Extensions, debugging UI, git integration |

## Plugins

| Plugin | Purpose |
|--------|---------|
| **oh-my-claudecode** | Multi-agent orchestration layer |
| **swift-lsp** | Swift Language Server Protocol support for iOS development |

## HUD (Heads-Up Display)

Custom statusline showing real-time agent activity:

```
node ~/.claude/hud/omc-hud.mjs
```

Displays: active mode, running agents, task progress, model usage — all in the terminal statusbar.

## My Workflow

A typical feature development flow:

```
1. Describe what I want          →  "autopilot: build a REST API for X"
2. OMC plans automatically       →  Explores codebase, creates plan
3. Agents execute in parallel    →  executor writes code, designer handles UI
4. Verification runs             →  architect reviews, tests pass
5. Ship                          →  /ship creates PR, runs CI
6. Monitor                       →  /canary watches production
```

## Philosophy

- **AI-native development** — AI is not an autocomplete; it's a team of specialists
- **Delegation over doing** — Route to the right agent at the right model tier
- **Verification before completion** — Never claim done without evidence
- **Multi-model consensus** — Use different AI models to cross-check critical decisions

---

*This is a living document. Updated as my stack evolves.*
