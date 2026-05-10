# TASK-016: Implement FHIR Catch-all Router (14-step orchestration)

**Phase:** 4 | **Agent:** `python-expert` (sonnet) | **Sub:** `backend-architect` (sonnet) | **GitHub Issue:** #5
**Depends on:** TASK-009, TASK-010, TASK-012, TASK-013, TASK-014, TASK-015
**Status:** todo

## Description
Implement `src/api/fhir_router.py` — catch-all route orchestrating the full 14-step happy path per spec §5.1.

## 14-step sequence
1. Extract/generate correlation ID
2. Extract `Authorization: Bearer <sp_token>`
3. Acquire PCM token (cached)
4. Introspect SP token → claims
5. Check cnf (warning-only)
6. Resolve national ID → patient_id
7. Mint internal ES256 JWT
8. Inject `_security:not` param
9. Forward to FHIR server
10. Verify response (forbidden label scan)
11. Enqueue audit event (non-blocking)
12. Return FHIR response

## Acceptance Criteria
- [ ] All 12 steps wired in correct order
- [ ] Missing `Authorization` header → `TokenMissingError` (DS-401 → HTTP 401)
- [ ] Any step failure → correct `OperationOutcome` returned
- [ ] Audit enqueued with `put_nowait()` (never awaited inline)

## QA Gate
```bash
pytest tests/integration/test_fhir_proxy.py::test_happy_path -v
# Uses respx for PCM mock, HAPI as real FHIR backend
```
