---
name: documentation-impact
description: Assess and maintain project documentation after a specific change. Use when asked to determine documentation impact or update the affected project knowledge; not for initial documentation setup.
---

# Documentation impact

Follow the user's scope and repository instructions. Preserve existing changes and read the documentation map, relevant current sources, applicable decisions and initiative plans, then inspect the change, connected implementation, schema, tests and configuration as needed.

Assess whether the change alters user or consumer behavior, architecture or module boundaries, data invariants, operations, durable decisions, or an initiative's execution context. Update only affected sources within authorized scope. Follow shared contracts to their owner and check relevant consumers; report inaccessible repositories and specific follow-up rather than asserting they were updated. Distinguish actual behavior, intent, plans and history. Investigate conflicts and report unresolved uncertainty; do not infer rationale or silently change a requirement to match potentially defective code.

Keep exact schema details in their authoritative source. Preserve historical documents and superseded decisions; if a durable decision changes, link its successor and update current truth separately. Update plans only for material initiative changes. An internal change with no semantic impact can require no documentation edits; state why.

Check changed links, status pointers and material claims against evidence. Review the diff for sensitive data and preserve unrelated work. Report the impact decision, files changed, checks, unresolved conflicts and any unverified consumers. Do not claim a spot check verifies the entire system.
