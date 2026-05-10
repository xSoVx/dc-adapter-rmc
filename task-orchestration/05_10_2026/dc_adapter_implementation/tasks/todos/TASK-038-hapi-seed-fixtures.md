# TASK-038: HAPI FHIR Seed Fixtures

**Phase:** 9 | **Agent:** `test-automator` (haiku) | **GitHub Issue:** #10
**Depends on:** TASK-037
**Status:** todo

## Description
Session-scoped pytest fixture that seeds required FHIR resources on HAPI and cleans up after test session.

## Resources to seed
- 1 Patient resource — normal (no security label)
- 1 Patient resource — with `meta.security Confidentiality=V`
- Tag all resources with unique run ID to avoid collision

## Acceptance Criteria
- [ ] Seed via `httpx.post("https://hapi.fhir.org/baseR4/Patient", ...)`
- [ ] Returns `{"normal_patient_id": "...", "confidential_patient_id": "..."}`
- [ ] Teardown: DELETE both resources (best-effort, no exception on failure)
- [ ] Run ID tag prevents collision with parallel CI runs

## QA Gate
```bash
pytest tests/integration/conftest.py --co -q
# fixture resolves without error
```
