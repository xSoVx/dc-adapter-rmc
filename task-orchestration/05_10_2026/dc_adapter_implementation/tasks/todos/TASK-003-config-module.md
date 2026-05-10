# TASK-003: Implement Config Module (pydantic-settings)

**Phase:** 1 | **Agent:** `python-expert` (sonnet) | **GitHub Issue:** #2
**Depends on:** TASK-001, TASK-002
**Status:** todo

## Description
Implement `src/config/__init__.py` using `pydantic-settings` v2. Load `config.yaml` as base, override with env vars using prefix `DS_ADAPTER_<SECTION>_<KEY>`. Secrets only via env — never in YAML.

## Sections required
`pcm`, `identity`, `fhir`, `jwt`, `audit`, `observability`, `logging`

## Acceptance Criteria
- [ ] `Settings()` loads defaults from `config.yaml`
- [ ] `DS_ADAPTER_FHIR_BASE_URL=x` overrides `fhir.base_url`
- [ ] Secret fields (`DS_ADAPTER_JWT_SIGNING_KEY` etc.) raise `ValueError` if accessed when empty
- [ ] No secret has a default value

## QA Gate
```bash
python -c "from src.config import Settings; s=Settings(); print('OK:', s.fhir.base_url)"
DS_ADAPTER_FHIR_BASE_URL=https://hapi.fhir.org/baseR4 python -c "from src.config import Settings; s=Settings(); assert 'hapi' in s.fhir.base_url; print('Override OK')"
```
