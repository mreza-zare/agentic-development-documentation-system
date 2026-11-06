---
name: living-documentation
description: Set up or maintain a project's agent-friendly living documentation. Use when asked to establish or improve a project documentation system. For a specific change, prefer the documentation-impact skill when available.
---

# Living documentation

Build a small, navigable knowledge base that reflects the project, and maintain it when its meaning changes. Follow the user's instructions and the repository's existing conventions and permissions.

## Start with evidence

- Inspect the relevant agent instructions, existing documentation, project structure, code, configuration, and tests. Read selectively; do not load the whole repository by default.
- Identify existing sources of truth, their audience, and any gaps or contradictions. Distinguish implemented behavior, intended behavior, and plans. Do not infer a product decision or claim an unverified fact. Investigate disagreements and report unresolved ones; ask the user when resolving one requires a decision.
- Preserve useful content and local changes. During setup or an explicitly requested reorganization, normalize equivalent documents to the base paths below and repair references; do not discard content to fit the structure. Use the project's language and existing tools.

## Practical guidance

For setup, migration, profile selection, or a non-obvious documentation impact, read [profiles and operating workflows](references/profiles-and-workflows.md). It defines required coverage, conditional documents, selection criteria, bootstrap and maintenance. For additional evidence and reconciliation guidance, see [the field guide](references/field-guide.md). For routine edits, use the concise workflow below.

## Set up

Establish these base files for every profile, keeping each concise when the project is small:

- Root `AGENTS.md`, or existing `CLAUDE.md`: state that documentation exists, point to `docs/index.md` and give the maintenance instruction below. Preserve existing instructions; both files are not required. If both exist, keep their documentation pointers consistent.
- `docs/index.md`: index all project documentation, including sources outside `docs/`, with real links, descriptions, audiences, reading triggers and current/planned/historical status.
- `docs/product.md`: purpose, users or consumers, problem, scope, capabilities, main workflows, rules and limitations. Separate current behavior from future plans.
- `docs/architecture.md`: technical structure, component responsibilities, dependencies, integrations, important boundaries and failure behavior. Link to separate module documents for detail; use `docs/modules/<module>.md` by default when the detail needs its own home.

Conditionally require `docs/database.md` at any profile when the repository owns or manages a database, its schema or migrations, or directly accesses a shared database with important data contracts. Cover ownership, main entities and relationships, invariants, lifecycle, access and migration constraints; link to authoritative schemas and migrations instead of copying exact fields. Link the document from architecture and the index. For a shared database, link to its owner's documentation and describe only the repository's own usage. A repository without a database role (such as an API-only frontend or stateless tool) needs no database document; explain the omission briefly in the setup report or architecture, without an empty file or broken link. See the [database documentation criteria](references/profiles-and-workflows.md#database-documentation).

During setup or an explicitly requested reorganization, rename a source with the same role and boundaries to its standard path and update links and instruction references. Split multipurpose sources into the appropriate homes while retaining other useful content. Reconcile an existing destination without overwriting local changes; ask when competing sources require an intent decision. Keep specialized sources in place and link to them instead of duplicating details. Flag external references you cannot update.

Document only evidence-backed knowledge useful to the project; mark unknowns and missing evidence rather than inventing content. Select a light, standard or heavy profile using the profiles guide. Profiles control depth and additional coverage, not whether the base files exist. Avoid empty templates and duplicating code, schemas or tests. Beyond the base files, add documents only for a clear purpose.

Keep these kinds of knowledge distinct; additional documentation can follow the project's conventions:

- **Current state:** product behavior, architecture, data rules, and other project-specific facts as they are now. Note evidence and uncertainty where useful.
- **Decisions:** durable choices and their rationale and consequences. Record a decision only when the why will matter later; preserve earlier decisions when they are superseded.
- **Plans:** intended or ongoing work and its execution context, clearly labeled as planned, in progress, or completed. Plans are not proof that behavior exists.
- **History:** use Git where available for complete change history. Preserve useful legacy material and label it historical rather than treating it as current.

In agent instructions, add a brief maintenance instruction: read the documentation index and relevant sources before work; after a meaningful change, assess documentation impact and update only affected knowledge. Keep the index complete when documents are added, renamed, removed or change status. Do not impose a new commit, approval, or other project workflow. Agent instruction discovery varies by tool, so explain any manual step needed for the user's agent.

## Tailor skills

During setup, identify only useful skills for the user’s recurring documentation workflows, following the selection criteria in [profiles and operating workflows](references/profiles-and-workflows.md). Prefer existing skills; propose none when none adds value. Create tailored skills when requested or authorized, within the appropriate project scope, and explain invocation and discovery.

## Maintain

For a focused post-change assessment, use the separate `documentation-impact` skill when available; the workflow below also works when it is not installed.

Maintenance alone does not authorize setup or migration to the base structure. Use the existing map and sources; report structural gaps without renaming files or creating base files merely to satisfy setup rules.

Read the map and the documents relevant to the task, then inspect code, schema, tests, or other evidence as needed. Assess whether product behavior, architecture, data rules, a durable decision, or an initiative's execution context has materially changed. Update the appropriate existing source with the smallest accurate edit; update `docs/database.md` when its ownership, entities, relationships, invariants, lifecycle, access or migration constraints change. If a change first introduces a database role, assess the conditional document within the requested scope rather than starting a full migration. Add a decision or plan only when justified. Preserve historical records, and do not turn plans into task diaries or changelogs.

An unchanged meaning is a valid no-op: report that no documentation update was required and why. When evidence is insufficient, say what is unknown instead of inventing a fact or decision.

## Verify and report

Check changed links and paths, accuracy against inspected evidence, preservation of existing material, and whether any new duplication is justified. Review the diff for credentials, personal data, and other information inappropriate for the destination. Report changed documents, any no-op, unresolved conflicts, and checks or limitations. Never expose sensitive findings in the report.
