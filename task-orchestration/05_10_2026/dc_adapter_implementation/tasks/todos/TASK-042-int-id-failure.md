# TASK-042: Integration — test_id_replacement_failure_returns_503

**Phase:** 9 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #10
**Depends on:** TASK-010, TASK-028
**Status:** todo

## Scenario
Mock ID replacement returns HTTP 500 on all 3 retries.

## Acceptance Criteria
- [ ] Adapter returns HTTP 503
- [ ] `OperationOutcome` code = `"DS-503"`
- [ ] Exactly 3 retry attempts in structlog output
- [ ] Jitter delays confirmed non-uniform (stddev > 0 from log timestamps)

## QA Gate
```bash
pytest tests/integration/test_error_paths.py::test_id_replacement_failure_returns_503 -v --timeout=30
```
