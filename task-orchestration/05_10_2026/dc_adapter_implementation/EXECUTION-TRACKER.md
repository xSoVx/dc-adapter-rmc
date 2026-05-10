# EXECUTION TRACKER — DC Adapter
**Started:** 2026-05-10 | **Target:** Connectathon 2026-05-10

---

## Progress Overview

| Phase | Tasks | Todo | In Progress | QA | Done |
|-------|-------|------|-------------|-----|------|
| 1 — Foundation | 5 | 5 | 0 | 0 | 0 |
| 2 — Auth | 3 | 3 | 0 | 0 | 0 |
| 3 — Introspection | 3 | 3 | 0 | 0 | 0 |
| 4 — FHIR Proxy | 6 | 6 | 0 | 0 | 0 |
| 5 — Audit | 4 | 4 | 0 | 0 | 0 |
| 6 — Observability | 4 | 4 | 0 | 0 | 0 |
| 7 — Errors | 4 | 4 | 0 | 0 | 0 |
| 8 — Unit Tests | 8 | 8 | 0 | 0 | 0 |
| 9 — Integration | 6 | 6 | 0 | 0 | 0 |
| 10 — Container | 4 | 4 | 0 | 0 | 0 |
| **TOTAL** | **47** | **47** | **0** | **0** | **0** |

---

## Task Movement Protocol
```
todos/  →  in_progress/  →  qa/  →  completed/
                               ↓
                          on_hold/  (if blocked)
```

Move file: `mv tasks/todos/TASK-NNN-*.md tasks/in_progress/`
After QA gate passes: `mv tasks/qa/TASK-NNN-*.md tasks/completed/`

---

## QA Gate Status per Phase

| Phase | Gate command | Status |
|-------|-------------|--------|
| 1 | `python -c "from src.config import Settings; s=Settings()"` | ⬜ |
| 2 | `pytest tests/unit/test_token_service.py -v` | ⬜ |
| 3 | `pytest tests/unit/test_introspection.py tests/unit/test_id_replacement.py -v` | ⬜ |
| 4 | `pytest tests/integration/test_fhir_proxy.py -v -k happy_path` | ⬜ |
| 5 | `pytest tests/unit/test_audit_service.py tests/unit/test_middleware.py -v` | ⬜ |
| 6 | `curl -sf http://localhost:8080/metrics \| grep dc_adapter_requests_total` | ⬜ |
| 7 | `pytest tests/unit/test_errors.py -v` + SIGTERM test | ⬜ |
| 8 | `pytest tests/unit/ --cov=src --cov-fail-under=80` | ⬜ |
| 9 | `pytest tests/integration/ -v --timeout=60` (3 consecutive runs) | ⬜ |
| 10 | `docker compose up -d && curl -sf http://localhost:8080/health` | ⬜ |

---

## EE Experiment Log

| Experiment | Phase | Variants | Winner | Playbook entry |
|-----------|-------|----------|--------|----------------|
| EXP-001: Retry backoff | 3 | uniform/full/decorrelated jitter | TBD | LL-001 |
| EXP-002: Proxy buffering | 4 | buffer-full / stream-inline | TBD | LL-002 |
| EXP-003: Audit queue | 5 | Queue+Task / create_task | TBD | LL-003 |
| EXP-004: OTel exporter | 6 | OTLP / Prometheus / both | TBD | LL-004 |
| EXP-005: Shutdown | 7 | asyncio.Event / asyncio.shield | TBD | LL-005 |
| EXP-006: Mock strategy | 8 | respx / unittest.mock / hybrid | TBD | LL-006 |
| EXP-007..011: Int scenarios | 9 | per scenario | TBD | LL-007..011 |
| EXP-012: E2E demo | 10 | — | — | LL-012 |

---

## Blocked / On Hold
_None yet_

---

## Model Cost Summary (estimated)
| Model | Agent usage | ~% of calls |
|-------|-------------|------------|
| opus | ace-agent (post-phase synthesis) | 10% |
| sonnet | python-expert, code-reviewer, ee-agent, security agents | 75% |
| haiku | test-automator, deployment-engineer | 15% |
