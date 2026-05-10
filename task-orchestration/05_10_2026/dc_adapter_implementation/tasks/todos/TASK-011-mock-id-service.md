# TASK-011: Implement Mock ID Replacement Service

**Phase:** 3 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #4
**Depends on:** TASK-001
**Status:** todo

## Description
Implement `src/identity/mock_id_service.py` — mountable FastAPI sub-app for local demo and integration tests.

## Acceptance Criteria
- [ ] `POST /api/v1/resolve` → `{"patient_id": "LOCAL-" + sha256(national_id)[:8]}`
- [ ] Same `national_id` always returns same `patient_id` (deterministic)
- [ ] Returns 404 for unknown format IDs

## QA Gate
```bash
uvicorn src.identity.mock_id_service:app --port 9001 &
curl -sf -X POST http://localhost:9001/api/v1/resolve \
  -H "Content-Type: application/json" -d '{"national_id":"IL-123"}' | python -m json.tool
kill %1
```
