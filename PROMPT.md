# Standalone prompt

Copy the prompt below into an agent working in your project. It does not require the skill or access to this repository. To assess a specific change instead of setting up the system, replace the first sentence with: “Assess the documentation impact of my current change; update only what is necessary.”

```text
Set up or improve an agent-friendly living documentation system for this project, and give future agents a concise way to maintain it. Follow my instructions, the project's conventions, and the permissions available to you.

If I requested only an assessment or maintenance, apply the relevant instructions below without starting an unsolicited setup or creating a map just to satisfy the setup procedure.

First inspect the relevant agent instructions, existing documentation, structure, code, configuration, and tests. Read selectively. Identify existing sources of truth, gaps, and conflicts. Distinguish implemented behavior from intended behavior and plans. Investigate discrepancies; report unresolved ones and ask me when a product or architectural decision is needed. Do not invent facts or decisions.

Preserve useful documentation and existing local changes. Do not overwrite, move, archive, or delete files merely to fit a new structure. Use the project's language and conventions. Create or improve a short documentation map in the existing entry point, or docs/index.md if none exists, linking only to real documents and explaining when to read them. Point existing agent instructions at the map, or create AGENTS.md if appropriate and within scope. Preserve existing instructions.

Document only evidence-backed knowledge useful to this project; prefer existing documents and avoid empty templates or duplicating details already reliably expressed by code, schemas, or tests. A small project may need only a map and one current-state document. Keep current behavior and constraints distinct from durable decisions and their rationale, plans and their status, and historical material. Use Git for complete history when available. Keep useful legacy records labeled as historical, and preserve superseded decisions.

Add a short maintenance instruction for future agents: read the map and relevant sources before work; after a meaningful change, assess the impact on documentation and make the smallest accurate update to the appropriate source. Create decisions or plans only when justified. If meaning has not changed, no documentation update is needed. Do not impose a new commit, approval, or other project workflow. Tell me if my agent needs a manual step to discover the instructions.

For setup or a non-obvious change, make the workflow concrete: inventory entry points, repository boundaries, owners, existing plans and decisions; trace representative behavior through code, tests, schema and configuration; and record evidence for important claims. Classify contradictions before resolving them: stale document, implementation defect, intentional divergence, or unknown. Do not change a requirement to match possibly defective code. For multiple repositories identify each boundary and its owner; verify accessible sources and report inaccessible ones without editing outside scope.

Make the map answer what to read and when, and mark existing, historical, planned and future sources clearly. Where the project warrants it, maintain separate product, architecture, data and operations knowledge; point to the schema for exact fields. Decisions should explain context, choice, rationale and consequences, preserving superseded records. Plans should show status, scope and dependencies and are not authorization or current truth. Preserve legacy material until useful knowledge has a confirmed home. Create domain notes only for a recurring need.

For maintenance, trace the change across user behavior, component boundaries, data invariants, operations, decisions and the relevant initiative. For example, an access-rule change may affect product and data docs; an internal refactor preserving behavior may require no update; a planned launch remains planned until supported by evidence. Check indexes and status pointers as well as content.

Verify changed links and paths, accuracy against inspected evidence, preservation of existing material, and justified duplication. Review the diff for credentials, personal data, and other information inappropriate for its destination. Report changes, no-op decisions, unresolved conflicts, and verification limits without exposing sensitive findings.
```
