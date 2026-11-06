# Agentic Development Documentation System

A small, adaptable method for creating and maintaining project documentation with a coding agent. It helps an agent find relevant knowledge, distinguish what exists from what is planned, and update documentation when the meaning of the system changes.

For this repository's complete documentation map, start at [docs/index.md](docs/index.md). See [product](docs/product.md) for purpose and behavior and [architecture](docs/architecture.md) for how the skills, prompt and references fit together.

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

For later changes, install the separate [`documentation-impact`](skills/documentation-impact/) skill using the same installer with its repository path, then ask `Use $documentation-impact to assess the documentation impact of this change.` The setup skill also supports this workflow if the separate skill is unavailable. Setup adds a concise documentation and maintenance pointer to the project's `AGENTS.md` or existing `CLAUDE.md`, but automatic discovery and adherence depend on the agent and its configuration.

The skill follows the [Agent Skills format](https://agentskills.io/specification). For another compatible agent, copy the [`skills/living-documentation`](skills/living-documentation/) directory to the location documented by that agent and invoke it as that agent requires. Installation paths and automatic invocation differ across tools. If your agent cannot load skills, use the [standalone prompt](PROMPT.md).

## How it works

1. Inspect the project's instructions, documents, and relevant implementation before proposing changes.
2. Establish the base files below and a map of all project documentation. Read only what a task needs.
3. Keep current state, durable decisions and their rationale, plans, and historical records distinct. Use existing documents where they fit.
4. After a meaningful change, assess documentation impact. Update the right source only when its meaning changed; an explicit no-op is a valid result.
5. Check the resulting links, evidence, diff, and destination-appropriate privacy before reporting the outcome.

Every profile uses these base files:

- Root `AGENTS.md`, or an existing `CLAUDE.md`: tell agents that documentation exists, point to the index and explain the maintenance workflow. Both files are not required; preserve existing instructions.
- `docs/index.md`: index all project documentation, including sources outside `docs/`, with a short description, audience, reading trigger and current/planned/historical status.
- `docs/product.md`: purpose, audience, problem, scope, capabilities, main workflows, rules and limitations; separate current behavior from future plans.
- `docs/architecture.md`: technical structure, component responsibilities, dependencies, integrations and important boundaries and failure behavior. Link to separate module documents for detail, using `docs/modules/<module>.md` by default when needed.

The method selects a light, standard, or heavy profile based on project architecture and coordination needs. Profiles change the depth and additional coverage, while retaining the base files. During setup or an explicitly requested reorganization, rename an existing document with the same role and boundaries to the standard path and repair references. Split multipurpose sources without losing useful content; link to existing detailed sources instead of copying them. Other documentation remains adaptable, and no ADR or saved plan is required for every task. Preserve local changes and investigate discrepancies rather than assume either the code or a document always wins. A focused maintenance assessment does not trigger a structural migration.

For profile selection, required and conditional documentation, and a step-by-step migration and maintenance process, see [profiles and operating workflows](skills/living-documentation/references/profiles-and-workflows.md). For a more detailed evidence workflow, including multi-repository ownership, evidence reconciliation, decisions, plans, and maintenance examples, see the [field guide](skills/living-documentation/references/field-guide.md). The standalone prompt includes the same core practices without requiring this repository.

The setup can also recommend a small set of project-specific agent skills when recurring workflows justify them. It reuses existing skills and creates tailored ones only when requested or authorized.

## Example

In a fictional small inventory app, an agent finds a README and an existing architecture note. During setup it renames that note to `docs/architecture.md`, fixes its references, and extracts product rules from the README into `docs/product.md` while retaining the README's quick start. It adds `docs/index.md` and points agent instructions to it. It does not create empty database or plans directories. A later internal refactor that preserves behavior needs no documentation edit; a change to a stock reservation rule updates the product document and any affected technical detail.

## Limits

The agent's output depends on its access, the evidence in the project, and human decisions. Review generated changes, especially conflicts and uncertain claims. A skill or instruction file cannot guarantee that every agent will discover or follow it, and it does not automatically run on every change. This project does not send project content to a service; the agent and tools you choose may have their own data-handling policies.

## Contributing

Open an issue or propose a focused pull request explaining the problem and how you checked the change. Keep examples fictional, omit private data and secrets, and prefer small changes that work across different projects. See [the skill](skills/living-documentation/SKILL.md) and [the standalone prompt](PROMPT.md) when changing the shared method so they remain consistent.

## License

[MIT](LICENSE).
