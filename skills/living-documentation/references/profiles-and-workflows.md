# Profiles and operating workflows

Use this guide when setting up or reassessing a documentation system. The profiles specify required **coverage**, not mandatory filenames. A project may combine topics in existing documents if each is easy to find and maintain. Never invent facts to fill a required section: mark unknowns and their evidence gaps.

## Select a profile

Inspect the project first: entry points and existing docs, code and tests, persisted data, deployment and operations, modules and repositories, and their owners and consumers. Identify trust boundaries, important workflows, failure recovery, and coordination costs. Recommend a profile with specific evidence, applicable conditional documents and omissions. If evidence is insufficient, state assumptions and revisit as understanding improves. The user can choose a different profile.

- **Light:** a small, cohesive project with few important workflows and limited operational or coordination needs. Minimum: shared essentials below.
- **Standard:** meaningful user journeys, data rules or operational concerns, or several significant components that require explanation, even in one monolith. Minimum: shared essentials plus separately discoverable product and architecture coverage.
- **Heavy:** multiple services, repositories, independently evolving modules or owners whose shared contracts and coordination are consequential. Repository count alone is not enough. Minimum: standard coverage plus an ownership and boundary map and shared-contract change process.

Architecture changes the content, not just the label. A monolith needs its internal layers and external boundaries explained when they matter. A modular monolith also needs important module responsibilities, dependency direction and contracts when those cannot be understood readily from code. A distributed system needs service boundaries, communication, failure and deployment ownership. A repository in a larger system can use a lighter profile than the whole system; link to the owning repository's verified contract rather than copying it. Reassess when scale, coupling, ownership or operational risk materially changes, not on every task.

## Documentation contract

The map must say what each source covers, when to read it and whether it is current, planned or historical. Link only existing accessible sources; identify unavailable sources as such. Agent instructions point to the map, say to inspect task-relevant evidence before work and assess documentation impact afterward, and preserve existing instructions. Do not promise automatic discovery by every agent.

Required shared coverage:

- **Entry point and map:** project purpose, links to actual sources, audiences and reading triggers; update when a destination, ownership or status changes. Avoid duplicating document contents.
- **Agent entry instructions:** where to start, relevant guardrails, evidence and maintenance workflow; update when discovery or the actual workflow changes. Do not copy project knowledge here.
- **Current state:** what the project does, its users or consumers, scope, major boundaries and known limitations, supported by code, tests, configuration or other reliable evidence. Separate intended behavior and unknowns. Update on semantic changes, not routine refactors.

Standard adds discoverable coverage of:

- **Product or service:** users/consumers, important workflows, roles, externally visible rules and scope. For libraries or infrastructure, describe consumers and supported contract instead of inventing end-user journeys. Update when behavior or scope changes; omit exhaustive screen or endpoint catalogs.
- **Architecture:** major components, responsibilities, dependencies, external integrations, trust boundaries and important failure behavior. Link to code and decisions; update when boundaries or integration semantics change. Avoid implementation inventories.

Heavy adds:

- **Ownership and contracts:** repository/service/module owners, system of record, producers and consumers, links to authoritative contracts, compatibility dependencies and how changes are verified across affected owners. Update when ownership, interface or compatibility changes. Do not duplicate schemas or claim unavailable consumers were verified.

Conditional coverage, required when the condition applies at any profile:

- **Data:** when persistent state or shared data has important invariants: source of truth, ownership, lifecycle, access and migration constraints, with links to schema/migrations. Update on invariant or ownership changes; exact columns stay in the schema.
- **Operations:** when setup, deployment, support or recovery has non-obvious steps: prerequisites, safe commands, verification and recovery, environment and owner. Update when the procedure changes; use placeholders for secrets and never expose credentials.
- **Decision records:** when a durable choice could be costly or unsafe to reverse without its rationale: context, decision, evidence-based reasons, consequences and status. Create only with known rationale; preserve and link superseded records. Do not infer historical reasons.
- **Initiative plans:** when work is long-running, multi-phase or has important dependencies: objective, scope, status, dependencies, milestones and verification. Update on material execution changes; planned work is not current behavior or authorization. No per-task diary.
- **Domain/module notes:** when a recurring complex domain or boundary cannot be navigated in the broader sources: responsibilities, invariants, contracts and evidence links. Update when those semantics change. Avoid one empty file per module.
- **Historical material:** when old specifications or context remain useful: label historical and link its successor or current source. Preserve it until useful knowledge has a confirmed home; correct historical errors rather than updating it as current truth.

Optional material, such as business context, design guidance or examples, belongs only when a real audience or recurring task benefits. For every new document state its audience, purpose, owner/source and reason an existing home is insufficient.

## Bootstrap an existing project

1. Check workspace status, instructions and permissions; inventory existing docs, active plans, code and sibling repositories. Preserve local edits and identify sources and owners. Do not assume documents or code always win conflicts.
2. Trace representative workflows and boundaries through implementation, tests, schema and configuration. Record evidence paths and unresolved questions. Distinguish observed behavior, intent, plans and history; classify conflicts as stale documentation, possible defect, intentional divergence or unresolved. Ask for a decision if intent cannot be established.
3. Recommend a profile and list required coverage: already covered, missing, conditional and unknown. Reuse existing sources; choose a migration order that makes the entry point and current truth usable first. Do not start unrelated product changes.
4. Add or improve the map, agent entry instructions and evidence-backed current coverage. Then add applicable conditional coverage and heavy-profile contracts. Mark unsupported facts unknown, name missing evidence and retain existing sources until valuable content has a confirmed home.
5. Validate links, evidence, statuses, user-facing instructions and discoverability. Report the profile and reason, changed sources, remaining gaps, conflicting evidence and inaccessible repositories. Do not call a migration complete merely because files exist.

## Select useful project skills

During setup, inspect the user's stated workflows, agent platform and existing project and user skills. Recommend only skills that address recurring tasks or a fragile procedure with concrete project-specific knowledge; a profile alone does not mandate a skill. Explain each recommendation, trigger, intended result, existing alternative and why a short instruction or existing skill is insufficient. No recommendation is a valid outcome.

Prefer reusing existing skills and instructions. Typical candidates, when justified by actual need, include documentation-impact assessment after meaningful changes, evidence-based reconciliation of stale documents, and cross-repository contract updates. A small project with occasional documentation edits may need none. Do not create separate skills for every document, module, profile or infrequent task, or embed changing system truth in skills; link to its owning source instead.

When the user asks for tailored skills or authorizes their creation, create only the selected skills in the agent's supported project location and within the authorized workspace. Each must have valid platform metadata, a narrow description and trigger, concrete steps, source links and verification; preserve existing skills. If the agent platform or installation location is unknown, report the proposed skill and ask only when that decision is necessary. Do not install into a user-wide location or alter agent configuration without authorization. Explain how the user invokes each skill and whether automatic discovery is supported, and validate the format and links. Reassess when workflows change; remove or consolidate redundant guidance only with appropriate authorization.

## Maintain during work

Before a task, follow the map to relevant current sources, applicable decision records and initiative plans, then inspect code and tests. After a meaningful task, decide whether the change affects product behavior, architecture or module boundaries, data invariants, operations, durable rationale or initiative context. Update each affected owner and its map pointers in the same change when authorized; if another repository cannot be edited, identify the exact follow-up and uncertainty. Preserve local edits and history.

- Access rule changed: update product and data invariants where relevant, verify against implementation and tests; record a decision only if its durable rationale changes.
- Shared contract changed: update its owner, check consumers and compatibility, and update boundary links and operational guidance as needed. Report consumers not checked.
- Durable decision replaced: add a successor with the new rationale, link and mark the old record superseded; update current truth separately.
- Internal refactor with no semantic or boundary change: make no documentation edit and report why. A completed small task does not complete an active initiative.

Review changed links and statuses, sample claims against evidence, check the diff for sensitive data and explain changes, no-op, gaps and checks. Never claim that a spot check proves all documentation correct.

## Worked selection examples

- A small single-purpose CLI with one repository and no persistent state: light; its README can cover map and current behavior, plus agent instructions. No data or plan document without a trigger.
- A student-facing monolith with important user journeys and access rules: standard; product and architecture coverage plus conditional data, operations and durable decisions as justified. The monolith label alone does not imply light.
- A modular monolith with independent domain boundaries and important dependency contracts: standard or heavy according to coordination cost; document meaningful module contracts without creating one document for every folder.
- A system with application, administration and shared database repositories: assess the whole system as heavy when contract coordination matters; each repository uses the profile its own responsibilities justify. The shared database owner documents the contract; consumers link to it and document their usage. Verify these relationships in the target project rather than assuming them from this example.
