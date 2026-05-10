# TASK-026: Implement Error Catalog (13 Codes)

**Phase:** 7 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #8
**Depends on:** TASK-001
**Status:** todo

## Description
Implement `src/errors/catalog.py` — all 13 error codes with HTTP status mappings and exception classes.

## Full catalog
| Code | HTTP | Exception class |
|------|------|-----------------|
| DS-400 | 400 | `ForbiddenLabelLeakedError` |
| DS-401 | 401 | `TokenMissingError` |
| DS-402 | 401 | `TokenInactiveError` |
| DS-403 | 403 | `AccessDeniedError` |
| DS-404 | 404 | `PatientNotFoundError` |
| DS-422 | 422 | `InvalidFHIRRequestError` |
| DS-500 | 500 | `InternalError` |
| DS-501 | 502 | `PCMTokenError` |
| DS-502 | 502 | `IntrospectionError` |
| DS-503 | 503 | `IdentityResolutionError` |
| DS-504 | 504 | `FHIRTimeoutError` |
| DS-505 | 502 | `FHIRUpstreamError` |
| DS-506 | 503 | `AdapterOverloadedError` |

## Acceptance Criteria
- [ ] Each exception carries `code` (DS-NNN) and `display` (generic text)
- [ ] `ERROR_CODE_TO_HTTP_STATUS` dict maps all 13 codes
- [ ] No exception message contains patient data

## QA Gate
```bash
pytest tests/unit/test_errors.py::test_all_13_error_codes_map_to_correct_http_status -v
```
