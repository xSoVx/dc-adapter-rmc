# TASK-039: Integration — test_happy_path_patient_search

**Phase:** 9 | **Agent:** `ee-agent`+`python-expert` (sonnet) | **Sub:** `api-security-audit` (sonnet) | **GitHub Issue:** #10
**Depends on:** TASK-038, TASK-016
**Status:** todo

## Description
Full adapter stack against HAPI FHIR. PCM mocked via respx.

## Scenario
- Valid SP token → mock introspect: `active=true, patient=IL-000001, consent_id=CONS-1, baskets=["medications"]`
- `GET /fhir/Patient?family=Smith&_count=5`

## Acceptance Criteria
- [ ] Returns 200 with FHIR Bundle from HAPI
- [ ] `_security:not=...|V` injected in forwarded request (respx captures params)
- [ ] Audit log entry has correct `consent_id` and masked `patient_id`
- [ ] `X-Correlation-ID` in response header

## QA Gate
```bash
pytest tests/integration/test_fhir_proxy.py::test_happy_path_patient_search -v --timeout=60
```
