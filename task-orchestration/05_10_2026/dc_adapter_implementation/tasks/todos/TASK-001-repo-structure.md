# TASK-001: Create Repository Structure per spec §3

**Phase:** 1 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #2
**Depends on:** — (first task)
**Status:** todo

## Description
Create the complete `src/` and `tests/` directory structure exactly as mandated by `spec-python.md §3`. Every directory must have an `__init__.py` stub.

## Acceptance Criteria
- [ ] `src/{main,config,api,auth,identity,fhir,audit,errors,observability,logging,middleware}/` exist
- [ ] `tests/{unit,integration}/` exist with `__init__.py`
- [ ] `pyproject.toml` created with `[tool.pytest.ini_options] asyncio_mode = "auto"`
- [ ] `.gitignore` covers `__pycache__`, `*.pyc`, `.env`, `certs/`

## QA Gate
```bash
python -c "import src.main" && echo PASS
```
