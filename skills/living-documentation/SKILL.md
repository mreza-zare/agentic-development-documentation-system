---
name: living-documentation
description: Set up or maintain a project's agent-friendly living documentation. Use when asked to establish a documentation system, assess documentation impact, or update project knowledge after a meaningful change.
---

# Living documentation

Build a small, navigable knowledge base that reflects the project, and maintain it when its meaning changes. Follow the user's instructions and the repository's existing conventions and permissions.

## Start with evidence

- Inspect the relevant agent instructions, existing documentation, project structure, code, configuration, and tests. Read selectively; do not load the whole repository by default.
- Identify existing sources of truth, their audience, and any gaps or contradictions. Distinguish implemented behavior, intended behavior, and plans. Do not infer a product decision or claim an unverified fact. Investigate disagreements and report unresolved ones; ask the user when resolving one requires a decision.
- Preserve useful existing documents and local changes. Do not overwrite, move, archive, or delete them merely to fit this method. Adapt to the project's language, naming, size, and existing tools.

## Practical guidance

For setup, migration, cross-repository work, or a non-obvious documentation impact, read [the field guide](references/field-guide.md). It contains an evidence workflow, concrete document shapes, and worked maintenance cases. For routine edits, use the concise workflow below.

## Set up

Create or improve a short documentation map using the project's existing entry point, or `docs/index.md` if there is none. Link only to real documents and describe when to read them. Add a concise pointer to the map in the project's existing agent instructions, or create `AGENTS.md` if appropriate and within the requested scope. Preserve existing instructions.

Document only knowledge justified by evidence and useful to the project. Use existing documents where possible; add a new document only when it has a clear purpose. A small project may need only a map and one current-state document. Avoid empty templates and duplicated details that code, schemas, or tests already express reliably.

Keep these kinds of knowledge distinct, without requiring a fixed directory tree:

- **Current state:** product behavior, architecture, data rules, and other project-specific facts as they are now. Note evidence and uncertainty where useful.
- **Decisions:** durable choices and their rationale and consequences. Record a decision only when the why will matter later; preserve earlier decisions when they are superseded.
- **Plans:** intended or ongoing work and its execution context, clearly labeled as planned, in progress, or completed. Plans are not proof that behavior exists.
- **History:** use Git where available for complete change history. Preserve useful legacy material and label it historical rather than treating it as current.

Where the project has agent instructions, add a brief maintenance instruction: read the documentation map and relevant sources before work; after a meaningful change, assess documentation impact and update only affected knowledge. Do not impose a new commit, approval, or other project workflow. Agent instruction discovery varies by tool, so explain any manual step needed for the user's agent.

## Maintain

Read the map and the documents relevant to the task, then inspect code, schema, tests, or other evidence as needed. Assess whether product behavior, architecture, data rules, a durable decision, or an initiative's execution context has materially changed. Update the appropriate existing source with the smallest accurate edit; add a decision or plan only when justified. Preserve historical records, and do not turn plans into task diaries or changelogs.

An unchanged meaning is a valid no-op: report that no documentation update was required and why. When evidence is insufficient, say what is unknown instead of inventing a fact or decision.

## Verify and report

Check changed links and paths, accuracy against inspected evidence, preservation of existing material, and whether any new duplication is justified. Review the diff for credentials, personal data, and other information inappropriate for the destination. Report changed documents, any no-op, unresolved conflicts, and checks or limitations. Never expose sensitive findings in the report.
