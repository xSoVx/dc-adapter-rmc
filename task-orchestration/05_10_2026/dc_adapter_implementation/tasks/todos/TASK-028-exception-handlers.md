# TASK-028: Register FastAPI Exception Handlers

**Phase:** 7 | **Agent:** `python-expert`+`code-reviewer` (sonnet) | **Sub:** `error-detective` (sonnet), `debugger` (sonnet) | **GitHub Issue:** #8
**Depends on:** TASK-027, TASK-016
**Status:** todo

## Description
Register FastAPI exception handlers in `src/errors/handlers.py` for all custom exceptions. Generic catch-all for unhandled exceptions → DS-500.

## Acceptance Criteria
- [ ] Each custom exception → correct HTTP status + OperationOutcome
- [ ] Unhandled exception → DS-500 + HTTP 500
- [ ] Full traceback logged at ERROR level to stderr
- [ ] `code-reviewer` completes `/code-review` before QA gate

## QA Gate
```bash
# DS-401 smoke test
curl -sf -o /dev/null -w "%{http_code}" http://localhost:8080/fhir/Patient
# expect 401
pytest tests/unit/test_errors.py::test_generic_exception_maps_to_ds500 -v
```
