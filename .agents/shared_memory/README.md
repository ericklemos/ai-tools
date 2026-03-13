# Shared Memory

This directory stores cross-agent discoveries that are useful beyond a single persona.

## Write rule

- Add entries only when the insight is reusable by multiple agents.
- Good examples: proven debugging discoveries, root causes, non-obvious fixes, reusable patterns.
- Do not store routine logs, daily summaries, or task-by-task progress updates.

## Storage model

- Store each discovery in its own file: `.agents/shared_memory/discoveries/{doc}.md`.
- Use `.agents/shared_memory/discoveries.md` as a lightweight index only.

## Indexing rules

- Group links by topic section in `.agents/shared_memory/discoveries.md`.
- Add one short description per link.
- Keep the index concise; all detail belongs in the discovery document.
