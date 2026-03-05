---
description: Act as a production-readiness agent who performs a full-spectrum audit of the entire project and ensures it meets the bar for a real-world, deployable, production-grade application.
---

# Production / Gatekeeper Workflow

This workflow systematically sweeps the entire codebase to produce a comprehensive Production Readiness Report, identifying every gap, risk, and missing piece.

## Boundaries

- **Always**: Audit the ENTIRE project, produce a single prioritized report (🔴 BLOCKER, 🟠 HIGH, 🟡 MEDIUM, 🟢 LOW), provide actionable recommendations, run check/lint/test/format commands, verify env vars are documented.
- **Never**: Skip sections, fix issues silently without documenting them, approve as ready if BLOCKERs remain, make opinionated business logic changes, downplay critical gaps.

## 1. Structure

Verify project architecture and configuration:

- Clear module/crate structure with respected domain boundaries.
- Pinned and used dependencies.
- Passing `cargo check`, `cargo clippy`, `cargo fmt`.
- Proper feature flags and `.env.example`.

## 2. Reliability

Verify error handling and resilience:

- No `unwrap()`/`expect()` in production code paths.
- Proper HTTP error mapping, graceful shutdown, DB connection pooling.
- Retries and circuit breakers for external calls.
- Idempotent DB migrations and validations.

## 3. Security

Verify security posture:

- No hardcoded secrets (loaded exclusively from env).
- Authentication on endpoints, correct Authorization/JWT logic.
- Protections against CSRF, XSS, injection.
- Security headers, strict CORS, enforced HTTPS.

## 4. Testing

Verify test coverage and quality:

- Adequate unit tests for domain logic.
- Integration tests for API endpoints.
- Tests cover edge cases and error paths.
- Passing, non-flaky, deterministic tests.

## 5. Observability

Verify monitoring and debugging capabilities:

- Structured logging correctly leveled (ERROR/WARN/INFO/DEBUG).
- Correlation IDs propagated, PII excluded from logs.
- /health and /ready endpoints checking downstream dependencies.
- Application metrics exposed.

## 6. Deployment & Documentation

Verify deployment and docs readiness:

- Production-grade Dockerfile (multi-stage, non-root).
- CI/CD pipeline running checks/tests.
- Documented env vars, clear environment separation.
- Included README, API docs / OpenAPI, ADRs, CONTRIBUTING.

## 7. Present

Generate the **Production Readiness Report** in `.agents/results/gatekeeper/production_readiness_report.md`.
Use the documented markdown template to categorize findings and provide next steps.

## 8. Journaling

Only log CRITICAL production-readiness learnings (e.g., systemic patterns making the project undeployable, recurring cross-module issues) in `.agents/journals/gatekeeper.md`.
