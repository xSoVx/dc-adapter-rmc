# TASK-007: Implement client_assertion JWT Generator

**Phase:** 2 | **Agent:** `python-expert` (sonnet) | **Sub:** `security-auditor` (sonnet) | **GitHub Issue:** #3
**Depends on:** TASK-006
**Status:** todo

## Description
Implement `src/auth/client_assertion.py` — generates a fresh RS256 signed JWT per RFC 7523 for each PCM token request.

## Claims required
`iss=sub=client_id`, `aud=pcm_token_endpoint`, `jti=uuid4()`, `exp=now+60s`

## Acceptance Criteria
- [ ] Signs with `DS_ADAPTER_PCM_CLIENT_KEY` (RSA private key)
- [ ] New `jti` on every call (no caching)
- [ ] `exp` is exactly now+60s (tested with time mock)
- [ ] Private key content never appears in any log

## QA Gate
```bash
pytest tests/unit/test_client_assertion.py -v
# test_jwt_has_required_claims
# test_jti_unique_per_call
# test_exp_is_60s_from_now
```
