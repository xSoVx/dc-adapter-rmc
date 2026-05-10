# TASK-027: Implement OperationOutcome Builder

**Phase:** 7 | **Agent:** `python-expert` (sonnet) | **Sub:** `security-auditor` (sonnet) | **GitHub Issue:** #8
**Depends on:** TASK-026
**Status:** todo

## Description
Implement `src/errors/operation_outcome.py` — builds FHIR R4 `OperationOutcome` JSON. System must be `http://ds-adapter/error-codes`.

## Output format
```json
{
  "resourceType": "OperationOutcome",
  "issue": [{
    "severity": "error",
    "code": "processing",
    "details": {
      "coding": [{"system": "http://ds-adapter/error-codes", "code": "DS-NNN", "display": "..."}]
    }
  }]
}
```

## Acceptance Criteria
- [ ] `system` is exactly `http://ds-adapter/error-codes`
- [ ] `display` is generic (no stack traces, no patient data, no internal errors)
- [ ] Full stack trace logged to stderr (not returned to client)

## QA Gate
```bash
pytest tests/unit/test_errors.py::test_operation_outcome_structure -v
pytest tests/unit/test_errors.py::test_no_stack_trace_in_response -v
```
