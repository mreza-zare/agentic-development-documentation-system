# Architecture

Status: current. Audience: contributors and coding agents changing this repository. This document owns the technical overview and artifact boundaries; detailed procedures remain in the linked skills and guides. See [product](product.md) for purpose and supported behavior and the [index](index.md) for all documentation.

## Structure and responsibilities

The repository is a Markdown instruction package with two skills, supporting references and a standalone prompt. It has no application runtime, database, build manifest or automatic documentation synchronizer.

- [README](../README.md) is the user entry point for installation, invocation and a short explanation of the method.
- [Living documentation](../skills/living-documentation/SKILL.md) is the setup and reorganization entry point, with a maintenance fallback. Its frontmatter supplies the skill name and discovery description.
- [Profiles and operating workflows](../skills/living-documentation/references/profiles-and-workflows.md) defines the base structure, profile depth, conditional coverage, migration and skill-selection rules. It is packaged with the setup skill.
- [Field guide](../skills/living-documentation/references/field-guide.md) supplies additional evidence, reconciliation, ownership and maintenance guidance within the setup skill package.
- [Documentation impact](../skills/documentation-impact/SKILL.md) is the separate focused-maintenance entry point. It contains the necessary guidance without requiring the setup skill to be installed.
- [Standalone prompt](../PROMPT.md) carries the core method without requiring skill loading or access to this repository. Its rules must remain consistent with both skills and the reference guides.

These existing sources provide component detail. Separate module files would duplicate them at this size. In target projects, architecture links to independent module documents when needed, using `docs/modules/<module>.md` by default or existing specialized sources.

## Execution and information flow

A user loads a skill or pastes the prompt into an agent working in a target project. The agent follows target-project instructions, permissions and language, then inspects relevant documents and implementation evidence. Setup selects a profile and establishes the base structure; focused maintenance assesses only the requested change and affected sources. Both workflows verify links and substantive claims and report unresolved uncertainty.

The setup skill reads its packaged reference guides for profile selection, migration or ambiguous work. The standalone prompt includes core practices directly because those guides may be unavailable to its consumer. This duplication supports independent delivery, so changes to shared rules require a parity review across the artifacts.

Within a documented project, root `AGENTS.md` or existing `CLAUDE.md` points to `docs/index.md`; the index routes readers to product, architecture and all other documentation. Architecture routes readers to module detail and authoritative contracts. All profiles use the same base filenames while varying depth and additional coverage. The [profiles guide](../skills/living-documentation/references/profiles-and-workflows.md) owns migration details.

## Boundaries and failure behavior

The agent and its tools perform all inspection and editing; this package does not enforce permissions, run hooks or send project content to a service. Agent discovery and compliance cannot be guaranteed by a Markdown instruction file. External agent and tool data-handling rules still apply.

Target code, schemas, tests and configuration provide evidence for current facts, while user decisions establish unresolved intent. Plans do not prove implementation. Contradictions require investigation, and inaccessible repositories or unverified claims must be reported instead of treated as checked. Shared contracts remain with their verified owner; consumers link to them rather than copying schemas.

This repository uses a light documentation profile: its components are instruction artifacts with no persistent application state or deployment workflow. The existing skill references provide sufficient component detail. More documentation is added only when evidence or recurring work justifies it.

## Change verification

When the method changes, check the skills, reference guides, standalone prompt and README for consistent requirements. Verify local links and index coverage, inspect migration cases and review the diff for content loss, unrelated changes and sensitive material. No runtime test suite or build pipeline is present in this repository; these checks validate the documentation artifacts and do not prove how every external agent will behave.
