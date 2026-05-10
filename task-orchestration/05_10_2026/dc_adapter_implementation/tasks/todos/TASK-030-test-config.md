# TASK-030: tests/unit/test_config.py

**Phase:** 8 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #9
**Depends on:** TASK-003, TASK-004
**Status:** todo

## Tests required (4)
- `test_defaults_loaded_from_yaml`
- `test_env_override_takes_precedence`
- `test_secret_not_in_yaml`
- `test_missing_required_secret_raises_on_use`

## QA Gate: `pytest tests/unit/test_config.py -v` — all pass, ≥80% coverage on `src/config/`
