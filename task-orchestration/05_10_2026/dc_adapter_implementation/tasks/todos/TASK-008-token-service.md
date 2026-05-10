# TASK-008: Implement PCM Token Cache

**Phase:** 2 | **Agent:** `python-expert` (sonnet) | **Sub:** `security-auditor` (sonnet) | **GitHub Issue:** #3
**Depends on:** TASK-006, TASK-007
**Status:** todo

## Description
Implement `src/auth/token_service.py` — async token acquisition with cache. TTL = `expires_in - token_ttl_margin_seconds`. Single-refresh lock for concurrent calls.

## EE Experiment (ee-agent, sonnet)
Test Variant A (asyncio.Lock) vs Variant B (asyncio.Event). Log PCM POST count under 10 concurrent callers.

## Acceptance Criteria
- [ ] First call: POST to `/oauth/token` → cache token
- [ ] Second call: returns cached token (0 additional POSTs)
- [ ] After expiry: refreshes on next call (no background thread)
- [ ] 10 concurrent calls → exactly 1 POST to PCM
- [ ] TTL = `expires_in - 5` (not hardcoded 5, uses config)

## QA Gate
```bash
pytest tests/unit/test_token_service.py -v --tb=short
# all 5 tests pass
```
