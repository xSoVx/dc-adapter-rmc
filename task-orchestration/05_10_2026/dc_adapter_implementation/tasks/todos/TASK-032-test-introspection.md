# TASK-032: tests/unit/test_introspection.py

**Phase:** 8 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #9
**Depends on:** TASK-009
**Status:** todo

## Tests required (5)
- `test_active_token_parsed_correctly`
- `test_inactive_token_raises_token_inactive_error`
- `test_cnf_mismatch_logs_warning_only` (no exception)
- `test_http_500_raises_introspection_error`
- `test_http_timeout_raises_introspection_error`

## QA Gate: all 5 pass, cnf test must NOT raise
