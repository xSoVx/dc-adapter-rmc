# TASK-018: Implement Correlation-ID Middleware

**Phase:** 5 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #6
**Depends on:** TASK-005
**Status:** todo

## Description
Starlette middleware that reads or generates `X-Correlation-ID` and binds it to structlog context.

## Acceptance Criteria
- [ ] Reads `X-Correlation-ID` from request; generates UUID4 if absent
- [ ] Stores on `request.state.correlation_id`
- [ ] Propagates as `X-Correlation-ID` response header
- [ ] `structlog.contextvars.bind_contextvars(correlation_id=...)` called
- [ ] Every log line in the request lifecycle includes `correlation_id`

## QA Gate
```bash
pytest tests/unit/test_middleware.py::test_correlation_id_generated_if_absent -v
pytest tests/unit/test_middleware.py::test_correlation_id_propagated_in_response -v
```
