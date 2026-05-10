# TASK-013: Implement FHIR Security Parameter Filter

**Phase:** 4 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #5
**Depends on:** TASK-001
**Status:** todo

## Description
Implement `src/fhir/security_filter.py` — injects `_security:not=http://fhir.health.gov.il/cs/il-core-main-security-label|V` into FHIR query params. Only for GET and `_search` requests.

## Acceptance Criteria
- [ ] GET `/fhir/Patient` → param injected
- [ ] POST `/fhir/Patient/_search` → param injected
- [ ] POST `/fhir/Patient` (non-search) → not injected
- [ ] PUT/DELETE/PATCH → not injected
- [ ] Existing `_security` param is appended, not replaced

## QA Gate
```bash
pytest tests/unit/test_security_filter.py -v
# all 5 tests pass, including test_existing_param_appended
```
