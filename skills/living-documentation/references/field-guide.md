# Field guide: living documentation in practice

Use this guide for setup, migration, cross-repository changes, or ambiguous maintenance. Keep the base filenames and conditional database filename defined in [profiles and operating workflows](profiles-and-workflows.md); adapt depth and additional documentation to the project.

## 1. Inventory and reconcile

1. Find agent instructions, entry points, existing documentation, active plans, and relevant repository boundaries. Check local changes before editing. Identify who owns each source and whether it is current, planned, or historical.
2. Trace representative user journeys and system boundaries through code, configuration, schema, and tests. For each important claim capture a path and, where useful, a symbol or test. Schemas establish structural details; implementation and tests help establish behavior; neither alone establishes product intent or rationale.
3. Classify discrepancies: stale documentation, implementation defect, intentional divergence, or unresolved. Investigate before editing. Do not silently rewrite a requirement to match an implementation that may be wrong. Report uncertainty and ask for a decision when evidence cannot resolve intent.
4. For multiple repositories, identify ownership of each boundary (application, administration, shared database, infrastructure, external services). Follow the actual source in each accessible repository. Link to stable sibling paths or repository URLs when available; explicitly mark inaccessible sources and avoid asserting their behavior. Do not edit sibling repositories outside the authorized scope.

## 2. Give each kind of knowledge a home

A useful `docs/index.md` answers **what to read and when**, not merely where files are. Index all project documentation, including sources outside `docs/`, with descriptions, audiences, reading triggers and current/planned/historical status. Root `AGENTS.md` or existing `CLAUDE.md` should point to the index and a short maintenance rule; preserve local workflow instructions and avoid copying the knowledge base into them. Both instruction files are not required; align pointers if both exist.

During setup or an explicitly requested reorganization, rename sources with the same role and boundaries to the base paths. Split multipurpose documents without losing other useful content, reconcile existing destinations without overwriting local changes, and repair incoming and outgoing links. Preserve specialized sources and link to them; flag external references you cannot update. See the profiles guide for migration examples.

Every profile has these separate current-state homes, concise for small projects:

- **Product (`docs/product.md`):** purpose, problem, users, roles, scope, capabilities, important journeys, visible rules and constraints. Identify gaps and future plans separately from implemented features.
- **Architecture (`docs/architecture.md`):** technical structure, component responsibilities, dependencies, trust boundaries, ownership, integration and failure behavior; link to code, decisions and separate module documents for detail.

Add these homes when their conditions in the profiles guide apply:

- **Database (`docs/database.md`):** required when the repository owns or manages a database, its schema or migrations, or directly accesses a shared database with important data contracts. Explain purpose, ownership, main entities and relationships, invariants, lifecycle, access and migration constraints; link to authoritative schemas, migrations and any shared database owner's documentation without maintaining a second schema. Link from architecture and the index. Repositories without a database role, such as API-only frontends or stateless tools, do not need the file; explain omission briefly in the setup report or architecture. See the [database documentation criteria](profiles-and-workflows.md#database-documentation) for migration and examples.
- **Other data:** document important non-database persistence or shared-data rules in an appropriate source. The presence of files, caches or logs does not by itself justify a database document.
- **Operations:** prerequisites, safe procedures, verification and recovery, with environment assumptions; never include secrets.
- **Decisions:** record context, decision, reasons and consequences when a durable choice could be wrongly reversed. Keep earlier decisions and link a successor when superseded. Do not invent rationale from code.
- **Plans:** record status, scope, dependencies, next meaningful milestone and verification for long-running work when useful. A planned initiative is neither current behavior nor permission to begin it. Update on material changes, not every commit.
- **History:** preserve useful original specifications and migration context, explicitly labeled historical; Git is normally the complete change history. Do not archive or remove a source until its valuable information has a confirmed home.

Put domain/module detail in separate documents when broad sources become difficult to use. Use `docs/modules/<module>.md` by default, reuse existing specialized sources where appropriate, and link them from architecture and the index. Avoid empty folders, exhaustive API or route copies, task diaries and repeated test counts.

## 3. Maintain after a change

Trace the change across user behavior, component boundaries, data invariants, operations, decisions and any initiative it actually belongs to. Inspect relevant current sources and their callers, then choose a destination:

For a focused assessment, use the existing map and sources even if the base structure is missing. Report structural gaps separately; maintenance alone does not authorize setup, file renames or a migration.

- A changed access rule updates product and data documents as needed; link to the implementation or schema, and update an ADR only if the durable decision itself changes.
- A shared schema ownership change may affect the owning repository and consumers' boundary descriptions; distinguish verified changes from inaccessible repositories and report work outside scope.
- An internal refactor preserving externally meaningful behavior and boundaries is normally a documented no-op.
- A future launch plan remains labeled planned; completing a local task does not make the initiative complete.

Update targeted sections rather than rewriting entire documents. If a prior decision is replaced, retain it and link the new record. Check links and status labels in maps and indexes as well as the edited document.

## 4. Verify the result

Follow changed local links and verify target existence, including case and relative paths. Sample substantive claims against the evidence gathered; distinguish verified current facts, proposed work, historical context, and unknowns. Check that entry points lead to relevant sources, no broken or contradictory status pointers were introduced, existing local changes remain intact, and the diff contains no secrets or private information. Report files changed, the evidence and checks used, any no-op and why, and unresolved conflicts or inaccessible sources. Do not claim all documentation is accurate based on a spot check.
