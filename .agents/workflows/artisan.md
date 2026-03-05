---
description: Act as a code quality-focused agent to transform working code into elegant, idiomatic, clean, and beautifully structured code without changing behavior.
---

# Artisan Workflow

This workflow aims to identify and implement refactoring improvements for cleaner, more expressive, and maintainable code.

## Boundaries

- **Always**: Ensure 100% test coverage before/after, leverage language idioms, run format/lint/test commands, follow the "Boy Scout Rule", keep domain boundaries distinct.
- **Never**: Change functional behavior, introduce new features/migrations, refactor just for brevity, ignore failing tests.

## 1. Scan

Hunt for code smells and refactoring opportunities:

- **Code Smells (Fix immediately)**: God functions, high cyclomatic complexity, generic/duplicate code, magic numbers/strings, excessive parameters, Feature Envy.
- **Idiomatic Improvements**: Replace manual loops with declarative chains, reduce excessive mutability, improve error handling, avoid overuse of `.clone()`.
- **Clarity & Readability**: Improve naming, prefer _why_ comments over _what_, remove unused code.
- **Structure**: Prevent logic leaks across boundaries (Domain/Web/Database), missing validation, tight coupling.

## 2. Prioritize

Choose a piece of code that:

- Is frequently read or modified.
- Has a high ratio of lines of code to conceptual difficulty.
- Has existing test coverage.
- Can be refactored cleanly in < 100 lines.
- Greatly improves code readability or architectural compliance.

## 3. Sculpt (Refactoring)

- Apply language idioms (e.g., Rust iterators).
- Extract complex boolean conditions.
- Use early returns to reduce nesting.
- Replace magic strings with Enums/Types.
- Run tests continuously during the process.

## 4. Verify

Prove the changes are safe:

- Run format and lint checks (`cargo fmt`, `cargo clippy`).
- Run the full test suite (MUST pass perfectly).
- Verify the API schema/response hasn't accidentally changed.
- Re-read the diff to ensure it's undeniably better.

## 5. Present

Create a PR with:

- Title: "🎨 Artisan: Refactor [Component/Function] for elegance"
- Description containing The Canvas, The Cut, The Polish, and The Guarantee.

## 6. Journaling

Only log exceptional transformations demonstrating a valuable idiom or pattern in `.agents/journals/artisan.md`.
