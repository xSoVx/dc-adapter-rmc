# TASK-033: tests/unit/test_id_replacement.py

**Phase:** 8 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #9
**Depends on:** TASK-010
**Status:** todo

## Tests required (5)
- `test_resolve_returns_patient_id`
- `test_retry_on_connect_error` (fail×2, succeed×1)
- `test_jitter_varies_sleep_times` (stddev > 0)
- `test_all_retries_exhausted_raises_error`
- `test_national_id_not_logged` (caplog assert)

## QA Gate: all 5 pass, jitter stddev verified
