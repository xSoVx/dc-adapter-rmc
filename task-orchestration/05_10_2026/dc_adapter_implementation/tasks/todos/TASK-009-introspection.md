# TASK-009: Implement PCM Token Introspection

**Phase:** 3 | **Agent:** `python-expert` (sonnet) | **Sub:** `api-security-audit` (sonnet) | **GitHub Issue:** #4
**Depends on:** TASK-008
**Status:** todo

## Description
Implement `src/auth/introspection.py` — POST to PCM `/oauth/introspect`, parse response into `IntrospectionResult` dataclass.

## IntrospectionResult fields
`active`, `patient`, `consent_id`, `baskets`, `access_type`, `sp_organization_id`, `cnf`

## Acceptance Criteria
- [ ] `active=false` → raises `TokenInactiveError` (DS-402 → HTTP 401)
- [ ] `cnf` mismatch → WARNING log only, no exception
- [ ] HTTP 5xx from PCM → raises `IntrospectionError` (DS-502 → HTTP 502)
- [ ] `national_id` / `patient` value never logged raw

## QA Gate
```bash
pytest tests/unit/test_introspection.py -v
# all 5 tests pass, including test_cnf_mismatch_is_warning_not_error
```
