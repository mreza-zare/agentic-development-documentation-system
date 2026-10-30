# Agentic Development Documentation System

A small, adaptable method for creating and maintaining project documentation with a coding agent. It helps an agent find relevant knowledge, distinguish what exists from what is planned, and update documentation when the meaning of the system changes.

## Quick start

Choose either the reusable skill or the [standalone prompt](PROMPT.md). The prompt works without installing a skill; paste it into an agent that can inspect and edit your project.

### Install the skill in Codex

In Codex, ask the skill installer:

```text
$skill-installer install https://github.com/mreza-zare/agentic-development-documentation-system/tree/main/skills/living-documentation
```

The installer places the skill in your Codex skills directory. Start a new Codex session if needed, then open the project you want to document and ask:

```text
Use $living-documentation to set up documentation for this project. Preserve existing documentation and explain any unresolved conflicts.
```

For later changes, ask `Use $living-documentation to assess the documentation impact of this change.` The setup also adds a concise maintenance pointer to project agent instructions when appropriate, but automatic discovery and adherence depend on the agent and its configuration.

The skill follows the [Agent Skills format](https://agentskills.io/specification). For another compatible agent, copy the [`skills/living-documentation`](skills/living-documentation/) directory to the location documented by that agent and invoke it as that agent requires. Installation paths and automatic invocation differ across tools. If your agent cannot load skills, use the [standalone prompt](PROMPT.md).

## How it works

1. Inspect the project's instructions, documents, and relevant implementation before proposing changes.
2. Create or improve a small map that points to the relevant sources. Read only what a task needs.
3. Keep current state, durable decisions and their rationale, plans, and historical records distinct. Use existing documents where they fit.
4. After a meaningful change, assess documentation impact. Update the right source only when its meaning changed; an explicit no-op is a valid result.
5. Check the resulting links, evidence, diff, and destination-appropriate privacy before reporting the outcome.

The method does not prescribe a fixed document tree or require an ADR or saved plan for every task. Existing documentation and local changes are preserved. An agent should investigate discrepancies rather than assume either the code or a document always wins.

For a more detailed workflow, including multi-repository ownership, evidence reconciliation, decisions, plans, and maintenance examples, see the [field guide](skills/living-documentation/references/field-guide.md). The standalone prompt includes the same core practices without requiring this repository.

## Example

In a fictional small inventory app, an agent finds a README and an existing architecture note. It adds a short map linking to both and documents a verified stock reservation rule in the appropriate existing note. It does not create empty database or plans directories. A later internal refactor that preserves the rule needs no documentation edit; a change to the rule does.

## Limits

The agent's output depends on its access, the evidence in the project, and human decisions. Review generated changes, especially conflicts and uncertain claims. A skill or instruction file cannot guarantee that every agent will discover or follow it, and it does not automatically run on every change. This project does not send project content to a service; the agent and tools you choose may have their own data-handling policies.

## Contributing

Open an issue or propose a focused pull request explaining the problem and how you checked the change. Keep examples fictional, omit private data and secrets, and prefer small changes that work across different projects. See [the skill](skills/living-documentation/SKILL.md) and [the standalone prompt](PROMPT.md) when changing the shared method so they remain consistent.

## License

[MIT](LICENSE).
