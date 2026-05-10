# TASK-021: Implement Multi-target Audit Service

**Phase:** 5 | **Agent:** `python-expert` (sonnet) | **Sub:** `performance-engineer` (sonnet) | **GitHub Issue:** #6
**Depends on:** TASK-020
**Status:** todo

## Description
Background asyncio.Task draining the audit queue and dispatching events to file, syslog, Kafka targets in parallel. Any target failure must not affect request.

## EE Experiment (ee-agent) — EXP-003
Variant A: asyncio.Queue + Task. Variant B: create_task() fire-and-forget per event. Metric: event loss rate, latency impact.

## Acceptance Criteria
- [ ] File: append JSON line to `config.audit.file_path`
- [ ] Syslog: UDP via `SysLogHandler`
- [ ] Kafka: `AIOKafkaProducer` — skipped gracefully if not configured
- [ ] Any target exception → WARNING log, continue (never re-raises)
- [ ] Flush on shutdown: drain queue max 5s

## QA Gate
```bash
pytest tests/unit/test_audit_service.py -v
# all 5 tests pass including test_queue_flushed_on_shutdown
```
