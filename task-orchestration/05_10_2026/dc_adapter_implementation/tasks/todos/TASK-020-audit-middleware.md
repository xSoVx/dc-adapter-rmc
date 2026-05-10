# TASK-020: Implement Audit Middleware (Enqueue)

**Phase:** 5 | **Agent:** `python-expert` (sonnet) | **Sub:** `performance-engineer` (sonnet) | **GitHub Issue:** #6
**Depends on:** TASK-018, TASK-019
**Status:** todo

## Description
After response sent: builds audit event dict and enqueues non-blocking via `asyncio.Queue.put_nowait()`. Never awaits inline.

## Audit event fields
`timestamp`, `correlation_id`, `method`, `path`, `sp_token_hash` (sha256), `patient_id_masked` (****last4), `consent_id`, `baskets`, `fhir_status`, `duration_ms`, `outcome`

## Acceptance Criteria
- [ ] `put_nowait()` used — never `await queue.put()`
- [ ] `patient_id` masked to `****XXXX` (last 4 chars only)
- [ ] `sp_token` hashed (sha256), never stored raw
- [ ] `include_response=false` by default

## QA Gate
```bash
pytest tests/unit/test_audit_service.py::test_patient_id_masked_correctly -v
pytest tests/unit/test_audit_service.py::test_audit_failure_does_not_fail_request -v
```
