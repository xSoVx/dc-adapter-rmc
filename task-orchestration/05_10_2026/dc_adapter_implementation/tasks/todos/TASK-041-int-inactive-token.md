# TASK-041: Integration — test_inactive_token_returns_401

**Phase:** 9 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #10
**Depends on:** TASK-009, TASK-028
**Status:** todo

## Scenario
Mock PCM introspection returns `{"active": false}`.

## Acceptance Criteria
- [ ] Adapter returns HTTP 401
- [ ] `OperationOutcome.issue[0].details.coding[0].code` = `"DS-402"`
- [ ] Zero FHIR upstream calls made (respx asserts no HAPI requests)

## QA Gate
```bash
pytest tests/integration/test_error_paths.py::test_inactive_token_returns_401 -v --timeout=30
```
