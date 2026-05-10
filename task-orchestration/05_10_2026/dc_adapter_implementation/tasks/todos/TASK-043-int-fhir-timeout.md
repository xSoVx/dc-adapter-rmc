# TASK-043: Integration — test_fhir_upstream_timeout_returns_504

**Phase:** 9 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #10
**Depends on:** TASK-014, TASK-028
**Status:** todo

## Scenario
Mock HAPI to raise `httpx.ReadTimeout`.

## Acceptance Criteria
- [ ] Adapter returns HTTP 504
- [ ] `OperationOutcome` code = `"DS-504"`
- [ ] Audit log records `outcome=error`, `fhir_status=null`

## QA Gate
```bash
pytest tests/integration/test_error_paths.py::test_fhir_upstream_timeout_returns_504 -v --timeout=30
```
