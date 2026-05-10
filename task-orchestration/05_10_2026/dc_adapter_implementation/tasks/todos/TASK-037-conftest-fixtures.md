# TASK-037: tests/conftest.py — Shared Fixtures

**Phase:** 8 | **Agent:** `test-automator` (haiku) | **GitHub Issue:** #9
**Depends on:** TASK-005
**Status:** todo

## Description
Create `tests/conftest.py` with session-scoped and function-scoped fixtures.

## Required fixtures
- `app_client` — `httpx.AsyncClient` via `ASGITransport(app=app)`
- `mock_pcm` — `respx` router mocking PCM token + introspect endpoints
- `mock_id_service` — `respx` router mocking ID replacement
- `test_ec_key_pair` — generated EC P-256 key pair (session-scoped)
- `test_rsa_key_pair` — generated RSA 2048 key pair (session-scoped)
- `audit_file` — tmp_path audit file path

## QA Gate
```bash
pytest tests/ --co -q | grep "conftest" || echo "Fixtures loaded OK"
pytest tests/unit/ -v --timeout=10 2>&1 | tail -5
```
