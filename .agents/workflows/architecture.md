---
description: Act as an architecture-focused agent to ensure the codebase aligns with strict structural rules, Domain-Driven Design (DDD), and CQRS principles.
---

# Architecture Workflow

This workflow ensures the codebase strictly adheres to its structural rules.

## Basic Architecture Rules

- **Domain Limits**: Pure Domain (`domain`) or Database (`database`) models must NEVER leak into HTTP requests/responses (`web`).
- **Data Transfer**: Always use intermediate DTOs and Validation Traits in the `web` layer.
- **CQRS**: Commands and Queries should be strictly separated.
- **TDD Requirement**: Any logic change must be test-driven (fail first, pass, refactor) with >80% coverage.

## 1. Analyze

Hunt for boundary leaks and structural debt in:

- **Web Layer**: Handlers returning/accepting Domain or Database models directly; missing DTOs; business logic inside the controller.
- **Domain Layer**: Domain entities containing database-specific logic or depending on web-specific types.
- **Database Layer**: Database queries residing outside the `database` crate or repositories.
- **Core/Shared**: Utilities in `core` that are domain-specific; duplicated validation logic.

## 2. Prioritize

Select the HIGHEST PRIORITY issue that:

- Clears up a boundary violation.
- Can be refactored cleanly.
- Has existing tests, or where tests can be written prior to refactoring (TDD).

Priority Order:

1. Boundary Violations
2. Logic misplacement
3. Missing DTOs or Validation Traits
4. File/Module organization within crates

## 3. Restructure

Implement the architectural fix:

- Create the necessary DTOs or mappings.
- Move logic to the appropriate layer/crate.
- Ensure TDD is respected.
- Update OpenAPI (`#[utoipa::path]`) and `.bru` files if web layer changes.

## 4. Verify

Test the structural integrity:

- Run `cargo fmt` and `cargo clippy`.
- Run `cargo test` to ensure >80% coverage and no broken logic.
- Verify that no new circular dependencies were formed.
- Check that the `domain` crate remains pure.

## 5. Present

Create a PR with:

- Title: "🏗️ Architect: [Architectural improvement/Refactor]"
- Description containing the Component, Violation, Alignment, and Testing sections.

## 6. Journaling (If Applicable)

If discovering a recurring architectural anti-pattern, a difficult boundary leak, or a specific interaction (e.g., Axum/Tokio/MongoDB) that affects DDD, document it in `.agents/journals/architect.md`.
