# MASTER COORDINATION — DC Adapter Implementation
**Date:** 05/10/2026 | **Project:** dc-adapter-rmc | **Connectathon:** 2026-05-10

---

## Orchestration Model

Three-agent system per `/start` command:
- **task-orchestrator** (`sonnet`) — Execution plan, dependency resolution, sequencing
- **task-decomposer** (`sonnet`) — Atomic task files, acceptance criteria
- **dependency-analyzer** (`haiku`) — Conflict detection, parallelization map

EE→ACE loop runs after each phase: `ee-agent` → `ace-agent` → `ee-ace-coordinator`

---

## Phase Map & Critical Path

```
Phase 1: Foundation ──────────────────────────────────────────── [TASK-001..005]
           │
Phase 2: Auth ────────────────────────────────────────────────── [TASK-006..008]
           │
Phase 3: Introspection & Identity ────────────────────────────── [TASK-009..011]
           │
Phase 4: JWT + FHIR Proxy ─────── (TASK-012 ──► TASK-013 ──► TASK-014 ──► TASK-015 ──► TASK-016..017)
           │
           ├── Phase 5: Middleware & Audit ───────────────────── [TASK-018..021]
           │                    │
           └── Phase 6: Observability ──────────────────────────  [TASK-022..025]
                                │
                           Phase 7: Errors & Shutdown ─────────── [TASK-026..029]
                                │
                     ┌──────────┴──────────┐
               Phase 8: Unit Tests     Phase 9: Integration Tests
               [TASK-030..037]         [TASK-038..043]
                     └──────────┬──────────┘
                                │
                           Phase 10: Container ─────────────────  [TASK-044..047]
```

---

## Parallelization Opportunities

| Can run in parallel | Tasks |
|---------------------|-------|
| After TASK-016 | TASK-018, TASK-022 (middleware & OTel independent) |
| After TASK-029 | TASK-030..037 (unit tests per module) |
| After TASK-037 | TASK-038..043 (integration scenarios) |

---

## Agent Assignments Summary

| Phase | Primary Agent | Model | Subagents |
|-------|--------------|-------|-----------|
| 1 — Foundation | `python-expert` | sonnet | `backend-architect` (sonnet) |
| 2 — Auth | `python-expert` | sonnet | `security-auditor` (sonnet), `api-security-audit` (sonnet) |
| 3 — Introspection | `python-expert` + `ee-agent` | sonnet | `api-security-audit` (sonnet) |
| 4 — FHIR Proxy | `python-expert` | sonnet | `backend-architect` (sonnet), `performance-engineer` (sonnet) |
| 5 — Audit | `python-expert` | sonnet | `performance-engineer` (sonnet) |
| 6 — Observability | `python-expert` | sonnet | `performance-engineer` (sonnet) |
| 7 — Errors | `python-expert` + `code-reviewer` | sonnet | `error-detective` (sonnet), `debugger` (sonnet) |
| 8 — Unit Tests | `python-expert` + `ee-agent` | sonnet | `test-automator` (haiku) |
| 9 — Integration | `ee-agent` + `python-expert` | sonnet | `test-automator` (haiku), `api-security-audit` (sonnet) |
| 10 — Container | `python-expert` + `code-reviewer` | sonnet | `deployment-engineer` (haiku) |
| QA Gates (all) | `code-reviewer` | sonnet | `security-auditor` (sonnet) |
| Knowledge loop | `ace-agent` | **opus** | `ee-ace-coordinator` (sonnet) |

---

## Resource Allocation Matrix

| Model | Tasks | Estimated token load |
|-------|-------|---------------------|
| opus | ace-agent knowledge synthesis (post each phase) | ~10% of total |
| sonnet | All implementation, review, security, debugging | ~75% of total |
| haiku | test scaffolding, Docker templates, dependency analysis | ~15% of total |

---

## FHIR Test Backend
All integration tests use: `https://hapi.fhir.org/baseR4`
PCM and ID Replacement: mocked via `respx`

---

## GitHub Issues
Epic: https://github.com/xSoVx/dc-adapter-rmc/issues/1
Phases: #2 (Foundation) → #11 (Container)
