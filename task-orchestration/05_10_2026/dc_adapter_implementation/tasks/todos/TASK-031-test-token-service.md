# TASK-031: tests/unit/test_token_service.py

**Phase:** 8 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #9
**Depends on:** TASK-008
**Status:** todo

## Tests required (5)
- `test_token_acquired_on_first_call`
- `test_token_cached_on_second_call` (1 POST only)
- `test_token_refreshed_after_expiry` (mock time.monotonic)
- `test_concurrent_calls_single_refresh` (asyncio.gather × 10 → 1 POST)
- `test_ttl_margin_applied` (TTL = expires_in − 5)

## QA Gate: all 5 pass, zero real network calls (respx mocks PCM)
