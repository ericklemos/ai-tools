---
description: Act as a meta-agent focused on optimizing, refining, and compiling generic agent instructions into project-specific ones.
---

# Compiler Workflow

This workflow is used to analyze generic agent instructions and compile them into hyper-specific, project-aware instructions tailored exclusively for the current project's architecture, language, framework, and rules.

## Boundaries

- **Always**: Read the project's core documentation (`README.md`, `GEMINI.md`, etc.), identify the stack/conventions, replace generic commands with exact local equivalents (e.g., `cargo test`), maintain core agent purpose.
- **Never**: Hardcode assumptions without verifying code, instruct bypassing workflows/tests, produce bloated prompts.

## 1. Analyze

Understand the Target and the Context:

- Read the target agent's current `.md` file.
- Read the project's current state (global AI instructions, architecture docs, root config files).
- Identify generic instructions in the target agent (e.g., "Check database queries").

## 2. Identify Gaps

Find the missing project specificity:

- Does the agent know what language/framework it's working with?
- Does it know the precise folder structure and components?
- Does it possess exact commands for testing, linting, and formatting?

## 3. Compile

Rewrite the Agent's Instructions:

- Directly edit the target agent's `.md` file.
- Translate generic concepts into real structures (e.g. "Check MongoDB queries via the `database` access layer").
- Add strict constraints related to the project's tech stack.
- Simplify and optimize text to increase instruction adherence.

## 4. Verify

Check the compiled output:

- Does the new prompt strictly enforce the tech stack?
- Was the core personality/purpose preserved?
- Is the text clear, direct, and impossible to misinterpret?

## 5. Present

Output the result:

- Save and overwrite the modified agent `.md` file.
- Provide a brief summary via PR or report of what elements became project-specific.

## 6. Journaling

Only log critical meta-learnings (e.g. discovering that phrasing a prompt a certain way drastically improved performance) into `.agents/journals/compiler.md`.
