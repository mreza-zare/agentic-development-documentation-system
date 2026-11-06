# Profiles and operating workflows

Use this guide when setting up or reassessing a documentation system. Every profile requires the base files below; profiles specify their depth and additional coverage. Additional topics may share a document when their boundaries remain clear, but product and architecture keep separate base files. Never invent facts to fill a section: mark unknowns and their evidence gaps.

## Select a profile

Inspect the project first: entry points and existing docs, code and tests, persisted data, deployment and operations, modules and repositories, and their owners and consumers. Identify trust boundaries, important workflows, failure recovery, and coordination costs. Recommend a profile with specific evidence, applicable conditional documents and omissions. If evidence is insufficient, state assumptions and revisit as understanding improves. The user can choose a different profile.

- **Light:** a small, cohesive project with few important workflows and limited operational or coordination needs. Minimum: shared essentials below.
- **Standard:** meaningful user journeys, data rules or operational concerns, or several significant components that require explanation, even in one monolith. Minimum: shared essentials with deeper product and architecture coverage as described below.
- **Heavy:** multiple services, repositories, independently evolving modules or owners whose shared contracts and coordination are consequential. Repository count alone is not enough. Minimum: standard coverage plus an ownership and boundary map and shared-contract change process.

Architecture changes the content, not just the label. A monolith needs its internal layers and external boundaries explained when they matter. A modular monolith also needs important module responsibilities, dependency direction and contracts when those cannot be understood readily from code. A distributed system needs service boundaries, communication, failure and deployment ownership. A repository in a larger system can use a lighter profile than the whole system; link to the owning repository's verified contract rather than copying it. Reassess when scale, coupling, ownership or operational risk materially changes, not on every task.

## Documentation contract

During setup or an explicitly requested reorganization, establish these base files:

- Root `AGENTS.md`, or existing `CLAUDE.md`: say that documentation exists, point to `docs/index.md` and describe the evidence and maintenance workflow. Preserve existing instructions. Both files are not required; keep pointers consistent if both exist.
- `docs/index.md`: index all project documentation, including sources outside `docs/`, with a description, audience, reading trigger and current/planned/historical status for each source. Link only existing accessible sources; identify unavailable sources as such. Update when documents are added, renamed, removed or change status.
- `docs/product.md`: purpose, users or consumers, problem, scope, capabilities, main workflows, rules and known limitations. Separate current behavior, plans and unknowns; update on semantic changes.
- `docs/architecture.md`: technical structure, component responsibilities, dependencies, integrations, important boundaries and failure behavior. Link to code, decisions and separate module documents for detail; default to `docs/modules/<module>.md` when needed.

Rename an existing source with the same role and boundaries to its standard path and repair links and instruction references. Split multipurpose sources while retaining useful content outside the base topics. Reconcile an existing destination without overwriting local changes; ask when competing sources require an intent decision. Keep specialized sources and link to them rather than copying details. Flag external references you cannot update. Agent instructions require reading task-relevant evidence before work and assessing documentation impact afterward; do not promise automatic discovery by every agent.

Required shared coverage:

- **Entry point and map:** project purpose, links to actual sources, audiences and reading triggers; update when a destination, ownership or status changes. Avoid duplicating document contents.
- **Agent entry instructions:** where to start, relevant guardrails, evidence and maintenance workflow; update when discovery or the actual workflow changes. Do not copy project knowledge here.
- **Current state:** what the project does, its users or consumers, scope, major boundaries and known limitations, supported by code, tests, configuration or other reliable evidence. Separate intended behavior and unknowns. Update on semantic changes, not routine refactors.

For light projects, the base files can be short, with known facts and explicit evidence gaps. Standard requires deeper coverage of:

- **Product or service:** users/consumers, important workflows, roles, externally visible rules and scope. For libraries or infrastructure, describe consumers and supported contract instead of inventing end-user journeys. Update when behavior or scope changes; omit exhaustive screen or endpoint catalogs.
- **Architecture:** major components, responsibilities, dependencies, external integrations, trust boundaries and important failure behavior. Link to code and decisions; update when boundaries or integration semantics change. Avoid implementation inventories.

Heavy adds:

- **Ownership and contracts:** repository/service/module owners, system of record, producers and consumers, links to authoritative contracts, compatibility dependencies and how changes are verified across affected owners. Update when ownership, interface or compatibility changes. Do not duplicate schemas or claim unavailable consumers were verified.

Conditional coverage, required when the condition applies at any profile:

- **Database (`docs/database.md`):** when the repository owns or manages a database, its schema or migrations, or directly accesses a shared database with important data contracts. Follow the [database documentation criteria](#database-documentation); this is conditional even for heavy profiles.
- **Other data:** when non-database persistent state or shared data has important invariants: source of truth, ownership, lifecycle, access and change constraints in an appropriate existing or justified document. Files, caches or logs alone do not require a database document.
- **Operations:** when setup, deployment, support or recovery has non-obvious steps: prerequisites, safe commands, verification and recovery, environment and owner. Update when the procedure changes; use placeholders for secrets and never expose credentials.
- **Decision records:** when a durable choice could be costly or unsafe to reverse without its rationale: context, decision, evidence-based reasons, consequences and status. Create only with known rationale; preserve and link superseded records. Do not infer historical reasons.
- **Initiative plans:** when work is long-running, multi-phase or has important dependencies: objective, scope, status, dependencies, milestones and verification. Update on material execution changes; planned work is not current behavior or authorization. No per-task diary.
- **Domain/module notes:** when a recurring complex domain or boundary cannot be navigated in the broader sources: responsibilities, invariants, contracts and evidence links, in separate documents linked from architecture and the index. Use `docs/modules/<module>.md` by default, reusing existing specialized sources when appropriate. Update when those semantics change. Avoid one empty file per module.
- **Historical material:** when old specifications or context remain useful: label historical and link its successor or current source. Preserve it until useful knowledge has a confirmed home; correct historical errors rather than updating it as current truth.

Optional material, such as supplementary business context, design guidance or examples, belongs only when a real audience or recurring task benefits. For every additional document state its audience, purpose, owner/source and reason an existing home is insufficient.

## Database documentation

Require `docs/database.md` at any profile if the repository owns or manages a database, its schema or migrations, or directly accesses a shared database with important data contracts. Inspect actual schemas, migrations and read/write flows; a database client dependency alone does not establish the need.

The document explains database purpose and ownership, main entities and relationships, invariants, lifecycle and retention, access boundaries and migration or compatibility constraints. Link to authoritative schemas and migrations for exact fields and to operational procedures for setup, backup or recovery; do not maintain a second schema or copy credentials. Update when these semantics change, and link the document from architecture and the index. For shared databases, keep the owner's documentation authoritative and document only this repository's use and constraints with links to the owner. Do not assert unverified behavior of inaccessible owners or consumers.

During setup or explicitly requested reorganization, apply the same preservation and reference-repair rules as for base files: rename an equivalent database document, split multipurpose sources without losing content, and retain specialized details with links. Focused maintenance uses an existing equivalent source without unsolicited renames. A change that first introduces a database role can justify adding this conditional document within the requested scope, without migrating the rest of the documentation.

Do not create the file where there is no database role. Explain the omission briefly in the setup report or architecture; do not add an empty document or an index link to a missing file. Examples:

- A backend owning relational tables, a CLI owning a SQLite database, or an infrastructure repository managing a database or its migrations needs `docs/database.md`, regardless of profile.
- A service directly reading or writing shared tables with important consistency or compatibility rules needs database documentation for its usage, linked to the authoritative owner.
- A frontend that only calls APIs, a stateless tool or a documentation-only repository does not need the file merely because another repository in the system has a database.
- Important file or object-storage rules still need data coverage when applicable, but do not automatically justify `docs/database.md`.

## Bootstrap an existing project

1. Check workspace status, instructions and permissions; inventory existing docs, active plans, code and sibling repositories. Preserve local edits and identify sources and owners. Do not assume documents or code always win conflicts.
2. Trace representative workflows and boundaries through implementation, tests, schema and configuration. Record evidence paths and unresolved questions. Distinguish observed behavior, intent, plans and history; classify conflicts as stale documentation, possible defect, intentional divergence or unresolved. Ask for a decision if intent cannot be established.
3. Recommend a profile and list required coverage: already covered, missing, conditional and unknown. Reuse existing sources; choose a migration order that makes the entry point and current truth usable first. Do not start unrelated product changes.
4. Establish the base files, migrating equivalent sources and repairing references as above. Then add applicable conditional coverage and heavy-profile contracts. Mark unsupported facts unknown, name missing evidence and retain existing sources until valuable content has a confirmed home.
5. Validate links, evidence, statuses, user-facing instructions and discoverability. Report the profile and reason, changed sources, remaining gaps, conflicting evidence and inaccessible repositories. Do not call a migration complete merely because files exist.

## Select useful project skills

During setup, inspect the user's stated workflows, agent platform and existing project and user skills. Recommend only skills that address recurring tasks or a fragile procedure with concrete project-specific knowledge; a profile alone does not mandate a skill. Explain each recommendation, trigger, intended result, existing alternative and why a short instruction or existing skill is insufficient. No recommendation is a valid outcome.

Prefer reusing existing skills and instructions. Typical candidates, when justified by actual need, include documentation-impact assessment after meaningful changes, evidence-based reconciliation of stale documents, and cross-repository contract updates. A small project with occasional documentation edits may need none. Do not create separate skills for every document, module, profile or infrequent task, or embed changing system truth in skills; link to its owning source instead.

When the user asks for tailored skills or authorizes their creation, create only the selected skills in the agent's supported project location and within the authorized workspace. Each must have valid platform metadata, a narrow description and trigger, concrete steps, source links and verification; preserve existing skills. If the agent platform or installation location is unknown, report the proposed skill and ask only when that decision is necessary. Do not install into a user-wide location or alter agent configuration without authorization. Explain how the user invokes each skill and whether automatic discovery is supported, and validate the format and links. Reassess when workflows change; remove or consolidate redundant guidance only with appropriate authorization.

## Maintain during work

Before a task, follow the index to relevant current sources, applicable decision records and initiative plans, then inspect code and tests. If the project has not adopted the base structure, use its existing map and sources; maintenance alone does not authorize setup or migration. Report structural gaps separately. After a meaningful task, decide whether the change affects product behavior, architecture or module boundaries, data invariants, operations, durable rationale or initiative context. Update each affected owner and its index pointers in the same change when authorized; if another repository cannot be edited, identify the exact follow-up and uncertainty. Preserve local edits and history.

- Access rule changed: update product and data invariants where relevant, verify against implementation and tests; record a decision only if its durable rationale changes.
- Shared contract changed: update its owner, check consumers and compatibility, and update boundary links and operational guidance as needed. Report consumers not checked.
- Durable decision replaced: add a successor with the new rationale, link and mark the old record superseded; update current truth separately.
- Internal refactor with no semantic or boundary change: make no documentation edit and report why. A completed small task does not complete an active initiative.

Review changed links and statuses, sample claims against evidence, check the diff for sensitive data and explain changes, no-op, gaps and checks. Never claim that a spot check proves all documentation correct.

## Worked selection examples

- A small single-purpose CLI with one repository and no persistent state: light; concise product and architecture base files, an index and agent instructions. Keep the README as a quick start linking to the index. No data or plan document without a trigger.
- A student-facing monolith with important user journeys and access rules: standard; product and architecture coverage plus conditional data, operations and durable decisions as justified. The monolith label alone does not imply light.
- A modular monolith with independent domain boundaries and important dependency contracts: standard or heavy according to coordination cost; document meaningful module contracts without creating one document for every folder.
- A system with application, administration and shared database repositories: assess the whole system as heavy when contract coordination matters; each repository uses the profile its own responsibilities justify. The shared database owner documents the contract; consumers link to it and document their usage. Verify these relationships in the target project rather than assuming them from this example.

## Migration examples

- **New project:** create the four base roles, using root `AGENTS.md` when neither agent instruction file exists. Write verified facts and explicit unknowns; do not create empty module files.
- **Equivalent source:** move a product-only `requirements.md` to `docs/product.md` only if it describes current product purpose and behavior with the same boundaries. Repair relative links inside the moved document and incoming references. A future-only specification remains a planned source linked from the product document and index.
- **Multipurpose source:** extract product and architecture sections from a README into their base files, retain installation and other useful material in the README, and replace extracted sections with links. Preserve plans and historical context with their labels.
- **Existing agent instructions:** update an existing `CLAUDE.md` to point to the index and maintenance workflow without creating `AGENTS.md`. If both exist, preserve both and align their documentation pointers.
- **Existing destination:** compare overlapping sources, consolidate verified content without loss and retain specialized material with links. Report unresolved disagreements instead of replacing one source silently.
- **Focused maintenance:** update an affected rule in an existing product source without renaming it or bootstrapping missing base files unless reorganization was also requested.
