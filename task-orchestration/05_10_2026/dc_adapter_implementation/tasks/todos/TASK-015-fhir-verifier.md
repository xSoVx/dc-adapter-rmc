# TASK-015: Implement FHIR Response Verifier

**Phase:** 4 | **Agent:** `python-expert` (sonnet) | **Sub:** `api-security-audit` (sonnet) | **GitHub Issue:** #5
**Depends on:** TASK-014
**Status:** todo

## Description
Implement `src/fhir/verifier.py` — scans every resource's `meta.security` in FHIR response for forbidden labels. Defense-in-depth after `_security:not` injection.

## Acceptance Criteria
- [ ] Parses Bundle `entry[*].resource.meta.security[]`
- [ ] Single-resource responses also checked
- [ ] `code=V` + correct system → raises `ForbiddenLabelLeakedError` (DS-400 → HTTP 400)
- [ ] Non-JSON / non-FHIR responses: pass through unchanged
- [ ] Zero patient data in raised exception message

## QA Gate
```bash
pytest tests/unit/test_fhir_verifier.py -v
# test_forbidden_label_raises_error
# test_clean_bundle_passes
# test_non_json_passes_through
```
