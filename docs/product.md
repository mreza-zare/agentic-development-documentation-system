# Product

Status: current. Audience: users adopting the method and contributors changing its behavior. This document owns product purpose, scope and rules; installation starts in the [README](../README.md) with tool-specific steps in the [installation guide](installation.md), and detailed agent procedures remain in the [sources indexed here](index.md).

## Purpose and audience

The Agentic Development Documentation System provides reusable instructions for creating and maintaining project knowledge with a coding agent. It serves developers and teams whose agents need to locate relevant documentation, distinguish current behavior from plans and retain useful context as a project changes.

The problem it addresses is scattered or stale knowledge: an agent can miss a source, treat a plan as implemented behavior, or update a document without checking the system it describes. The method uses selective inspection, explicit evidence and a navigable index to reduce these errors.

## Current capabilities and workflows

- **Setup or reorganization:** inspect instructions, existing documents and implementation evidence; select a documentation profile; establish base files; migrate equivalent sources without losing content; add conditional coverage when justified; verify the result.
- **Focused maintenance:** inspect a meaningful change and relevant knowledge, update affected sources and index entries, or explain why unchanged meaning needs no edit. Report structural gaps without starting an unsolicited migration.
- **Alternative delivery:** use the setup skill, the dedicated maintenance skill or the self-contained standalone prompt. Installation and discovery depend on the user's agent.
- **Complex projects:** follow ownership and shared contracts across accessible repositories, preserve historical decisions and identify work that cannot be verified within the authorized scope.
- **Tailored workflows:** recommend project-specific skills only for real recurring needs; create them only when requested or authorized.

## Product rules

All profiles require root `AGENTS.md` or existing `CLAUDE.md`, plus `docs/index.md`, `docs/product.md` and `docs/architecture.md`. The index covers all project documentation, including sources elsewhere in the repository. Product and architecture keep separate responsibilities; module details have separate linked sources when needed. The [profiles guide](../skills/living-documentation/references/profiles-and-workflows.md) owns the full contract and migration cases.

Light, standard and heavy profiles adjust depth and coordination coverage. Small projects still have the base files, with concise verified content and explicit unknowns. Additional data, operations, decision, initiative or module documents depend on the project's actual needs.

`docs/database.md` is conditional at every profile: it is required when a repository owns or manages a database, its schema or migrations, or directly accesses a shared database with important data contracts. It covers ownership, main entities and relationships, invariants, lifecycle, access and migration constraints, linking to authoritative schemas rather than duplicating them. Repositories without that role, including API-only frontends and stateless tools, do not need it. The [database documentation criteria](../skills/living-documentation/references/profiles-and-workflows.md#database-documentation) define inclusion, omission and migration behavior.

Preserve useful content, existing instructions and local changes. During setup or requested reorganization, rename genuinely equivalent sources and repair references; split documents with multiple responsibilities without discarding their other material. Keep specialized knowledge in its existing authoritative source where possible.

Document current behavior separately from intended behavior, plans and history. Investigate disagreements rather than assuming code or documents always win. Unknown intent requires a decision; unsupported facts and historical rationale must not be invented. Semantic changes drive maintenance, not a requirement to edit documentation on every task.

## Boundaries and limitations

This repository distributes Markdown instructions. It does not contain a runtime that monitors projects, automatically invokes agents, migrates files or synchronizes documentation. Instruction discovery, execution, access and data handling depend on the chosen agent and tools.

The method does not guarantee correctness or universal agent compliance. Its output depends on available evidence, permissions and human decisions. Verification limits and inaccessible sources must be reported. Setup does not authorize unrelated product changes, user-wide installations or new commit and approval workflows.

## Future work

This document makes no commitment to unimplemented capabilities. Future proposals should be labeled planned and linked from the [index](index.md); they do not become current behavior or permission to execute merely by being documented.
