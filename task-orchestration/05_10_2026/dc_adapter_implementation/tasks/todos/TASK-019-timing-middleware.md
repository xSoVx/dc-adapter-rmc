# TASK-019: Implement Timing Middleware

**Phase:** 5 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #6
**Depends on:** TASK-018
**Status:** todo

## Description
Starlette middleware that records request start time and logs `duration_ms` after response.

## Acceptance Criteria
- [ ] `time.perf_counter()` captured at entry
- [ ] `duration_ms` emitted as structlog INFO after response
- [ ] Stored on `request.state.start_time` for audit access
- [ ] Does not add > 0.5ms overhead (tested)

## QA Gate
```bash
pytest tests/unit/test_middleware.py::test_timing_duration_logged -v
```
