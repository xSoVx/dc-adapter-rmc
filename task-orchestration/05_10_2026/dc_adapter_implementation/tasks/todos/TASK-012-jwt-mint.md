# TASK-012: Implement Internal ES256 JWT Minter

**Phase:** 4 | **Agent:** `python-expert` (sonnet) | **Sub:** `security-auditor` (sonnet) | **GitHub Issue:** #5
**Depends on:** TASK-009, TASK-010
**Status:** todo

## Description
Implement `src/auth/jwt_mint.py` — mint an ES256-signed JWT carrying all consent context for forwarding to the FHIR server.

## Required claims (all 9 mandatory)
`iss`, `aud`, `sub` (patient_id), `exp`, `iat`, `jti`, `consent_id`, `baskets[]`, `access_type`, `sp_org`

## Acceptance Criteria
- [ ] Algorithm: ES256 using `DS_ADAPTER_JWT_SIGNING_KEY` (EC private key)
- [ ] New `jti` per mint (uuid4)
- [ ] `exp = now + config.jwt.ttl_seconds`
- [ ] All 9 claims present (verified by decoding in test)
- [ ] Key content never logged

## QA Gate
```bash
pytest tests/unit/test_jwt_mint.py -v
# test_all_9_claims_present
# test_exp_correct_ttl
# test_es256_algorithm_used
```
