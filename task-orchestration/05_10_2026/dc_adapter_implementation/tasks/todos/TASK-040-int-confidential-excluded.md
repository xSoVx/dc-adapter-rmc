# TASK-040: Integration — test_confidential_resource_excluded

**Phase:** 9 | **Agent:** `ee-agent`+`python-expert` (sonnet) | **Sub:** `api-security-audit` (sonnet) | **GitHub Issue:** #10
**Depends on:** TASK-038, TASK-015
**Status:** todo

## Description
Test that Confidentiality=V resources are excluded. Documents actual HAPI R4 behavior.

## EE Experiment — EXP-009
- Variant A: HAPI respects `_security:not` → resource absent from response
- Variant B: HAPI ignores IL labels → adapter verifier catches it → 400 DS-400
Both outcomes acceptable; correct handling required.

## Acceptance Criteria
- [ ] Resource with `Confidentiality=V` does NOT appear in final response
- [ ] Either path (HAPI excludes OR adapter verifier rejects) is correct
- [ ] Behavior documented in test docstring with actual HAPI response noted

## QA Gate
```bash
pytest tests/integration/test_fhir_proxy.py::test_confidential_resource_excluded -v --timeout=60
```
