# Installation and tool setup

Status: current. Audience: developers and teams adding this method to their coding agent. Tool documentation and adoption sources were checked on **2026-11-06**. This guide covers installing this repository's instructions into an existing tool; use the linked vendor documentation to install the tool itself.

## Choose your tool

- [Managed installation (recommended)](#managed-installation-recommended)
- [Update through your agent](#update-through-your-agent)
- [Claude Code](#claude-code)
- [ChatGPT and Codex](#chatgpt-and-codex)
- [Cursor](#cursor)
- [Google Antigravity](#google-antigravity)
- [OpenCode](#opencode)
- [Other agents and the standalone prompt](#other-agents-and-the-standalone-prompt)

Coverage is limited to these five requested tools. Recent adoption evidence also supports their inclusion: in the [Stack Overflow 2026 survey's coding-agent question](https://survey.stackoverflow.co/2026/ai/data/#ai-code-agent), 12,255 respondents reported past-year use of Claude Code (65.5%), Codex (29.5%), Cursor (25.5%), Antigravity (16.0%) and Open Code (13.6%). Multiple choices were allowed; these figures describe that survey sample, not current market share or a ranking of all tools. Installation details below come from current official documentation, not those survey results.

## What to install

The repository provides two independent skills:

- [`living-documentation`](../skills/living-documentation/SKILL.md): initial setup, migration or a requested reorganization, with a maintenance fallback.
- [`documentation-impact`](../skills/documentation-impact/SKILL.md): focused maintenance after a meaningful change.

Install both if you want both workflows. Use the managed installation below for repeatable updates. For manual installation, copy each **whole skill directory**, including the setup skill's `references/` directory. Copying only `SKILL.md` breaks its reference links. Keep the directory names unchanged.

For manual installation, [download this repository](https://github.com/mreza-zare/agentic-development-documentation-system/archive/refs/heads/main.zip) and extract it, or clone it into a separate location:

```sh
git clone https://github.com/mreza-zare/agentic-development-documentation-system.git
```

The source directories are `skills/living-documentation/` and `skills/documentation-impact/` inside that download or clone. In the sections below, copy both into your chosen destination. For example, a project installation for Claude Code should produce:

```text
your-project/
  .claude/skills/
    living-documentation/
      SKILL.md
      references/
        profiles-and-workflows.md
        field-guide.md
    documentation-impact/
      SKILL.md
```

Project paths are relative to the **project you want to document**, not necessarily this repository. User paths apply across projects on the machine where the agent runs. `~` means your home directory; on Windows, use your user-profile directory (PowerShell: `$HOME`). Prefer project scope for a shared team setup. Choose one location per tool and scope to avoid duplicate skill names; where tools support the same `.agents/skills/` directory, a single project copy can serve them.

## Managed installation (recommended)

[Skills CLI](https://github.com/vercel-labs/skills) records the source of an installation so it can check for and apply updates. It requires **Node.js 22.20 or later and npm/npx**, Git access to the source repository, and a supported local agent. This is an external package manager, not a background service shipped by this repository. See its [command reference](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) for current options.

From the project you want to document:

```sh
npx skills add mreza-zare/agentic-development-documentation-system --skill living-documentation documentation-impact
```

Choose the intended agent and installation method. The default scope is the current project; add `-g` for a user-wide installation. Symlinks share a canonical copy; `--copy` is available where symlinks are unsuitable. Keep the manager's lock metadata so future updates can identify the source. For project installations, review and commit the installed files and lock metadata according to that project's conventions.

When an agent needs a non-interactive command, explicitly target the requested agent, for example a project installation for Codex:

```sh
npx skills add mreza-zare/agentic-development-documentation-system --skill living-documentation documentation-impact --agent codex -y
```

Other supported agent identifiers include `claude-code`, `cursor`, `antigravity` and `opencode`. Install only to the requested agent and scope. The tool-specific sections below describe invocation and alternative manual locations; do not also copy the same skills into another discovery directory. An installation in a local agent does not install into every ChatGPT or cloud session.

## Update through your agent

Users can copy the [update request in the README](../README.md#update-through-your-agent) into their coding agent. The agent should follow this procedure:

1. Inspect the target project's instructions, the active agent's discovery locations, installed copies of these two skills, and Skills CLI lock metadata at the intended project or user scope. Resolve symlinks before editing. Confirm that tracked entries refer to `mreza-zare/agentic-development-documentation-system`; a matching skill name alone does not establish ownership. If multiple active copies or scopes make the destination ambiguous, ask which installation to update.
2. Compare installed contents with their recorded upstream revision where available. Preserve local customizations and back up the two complete installed directories and relevant lock metadata outside skill discovery locations before replacement. If no trustworthy baseline exists, retain the old contents and compare them with a fresh upstream copy; do not assume differences are disposable. Ask before resolving conflicting customizations.
3. For a verified managed installation, run the applicable scoped command below. Update only the names owned by this repository. `npx skills check` is an optional read-only check for available updates across tracked skills; it is not required for a targeted update. A nonzero check result can mean updates are available, so inspect the output.

```sh
# Project installation: run from the target project
npx skills update living-documentation documentation-impact -p

# User-wide installation: use this instead of the project command
npx skills update living-documentation documentation-impact -g
```

4. Inspect the command's output and resulting files; do not infer success from the exit code alone. Confirm both `SKILL.md` files and `living-documentation/references/profiles-and-workflows.md` and `field-guide.md` are present, check their relative links, and verify the installed contents against the fetched upstream revision. Reconcile preserved customizations explicitly. If the manager skipped a missing skill or the wrong source/scope, repair only that installation rather than reporting success.
5. Verify discovery in the intended agent, refreshing or restarting as needed. Report changed paths, project/user scope, source revision (and any pin retained), preserved customizations, verification limits and recovery location. If validation fails, restore the affected skill directories and changed lock metadata from backup. Do not modify generated project documentation or rerun setup as part of a package update.

The unpinned installation command follows the repository's default branch; "latest" means the latest available upstream content, not a promised release version. If an installation is pinned to a tag or commit, report the pin and ask before moving it. Publishing a commit does not push updates to users: they must request or run an update. Existing sessions may still hold earlier instructions until refreshed.

### Previous manual or Codex installer installations

Copies made manually or by Codex's built-in `$skill-installer` are not automatically tracked by Skills CLI. Repeating the built-in installation is not an update procedure; its current installer refuses an existing destination. There is no retroactive automatic migration.

For a one-time migration, the agent should:

1. Locate the active copies and intended scope as above. Back up their complete directories and any existing manager lock metadata outside discovery locations; compare with a fresh upstream copy and preserve customizations.
2. Move only the verified old copies of these two skills outside discovery locations, then run the managed installation command for the same intended agent and scope. Inspect the manager's resulting paths rather than assuming they match the old installer paths. Keep unrelated skills untouched.
3. Verify contents, references, source tracking and discovery, reconcile customizations, and ensure an old copy does not shadow the new one. Keep the backup available. If installation fails, restore the old copies and prior metadata before reporting the failure.

If Node.js/npm or managed installation is unavailable, refresh manually: obtain a fresh download or clone, record its revision when available, compare and reconcile each complete skill directory, then replace only these two installed directories using the same backup and verification steps. Replace the complete directories so removed upstream files do not linger. A manual refresh remains a manual installation; do not claim it is now tracked by Skills CLI. A user of the standalone prompt should fetch the latest `PROMPT.md` for their next session.

### Scope and recovery

An update changes reusable instructions and packaged references. Existing `AGENTS.md`, `CLAUDE.md` and generated project documents remain project-owned; adopting changed method rules in them is a separate requested documentation task. Treat customizations as local project knowledge, not upstream defects. Keep backups outside discovery paths to prevent duplicate skill names. Do not delete or overwrite unrelated skills, instruction files or project documents.

## Claude Code

Copy both skill directories into either:

- Project: `.claude/skills/`
- User: `~/.claude/skills/`

Open Claude Code in the target project and type `/` to check that both skills are listed. Invoke setup:

```text
/living-documentation Set up documentation for this project. Preserve existing documentation and explain any unresolved conflicts.
```

After a later change:

```text
/documentation-impact Assess the documentation impact of this change and update only affected sources.
```

These paths describe local repository sessions. Cowork and cloud sessions have separate loading rules; a personal folder on your machine does not automatically reach them. See the official [Claude Code skills guide](https://code.claude.com/docs/en/skills).

## ChatGPT and Codex

Prefer [managed installation](#managed-installation-recommended) if you want the update commands above. As an alternative first installation in Codex, ask its built-in installer to install each skill:

```text
$skill-installer install https://github.com/mreza-zare/agentic-development-documentation-system/tree/main/skills/living-documentation
```

```text
$skill-installer install https://github.com/mreza-zare/agentic-development-documentation-system/tree/main/skills/documentation-impact
```

For manual local discovery, copy both directories into `.agents/skills/` in the target project or `~/.agents/skills/` for your user. Check the available skills; restart Codex if a new skill is missing. In the CLI or IDE extension, use `/skills` or type `$`, then ask:

```text
Use $living-documentation to set up documentation for this project. Preserve existing documentation and explain any unresolved conflicts.
```

```text
Use $documentation-impact to assess the documentation impact of this change and update only affected sources.
```

In ChatGPT, skill selection uses `@` where supported. The local folders above describe Codex discovery; they do not install a skill into every ChatGPT session. This repository ships plain skill folders, without a plugin manifest. Use the standalone prompt when your session cannot load them. See the official OpenAI documentation on [building and using skills](https://learn.chatgpt.com/docs/build-skills).

## Cursor

Copy both directories into either:

- Project: `.cursor/skills/` (or the shared `.agents/skills/`)
- User: `~/.cursor/skills/` (or `~/.agents/skills/`)

In Agent chat, type `/` and select `living-documentation` for setup or `documentation-impact` for a later change. Add the task after selecting it, for example:

```text
/living-documentation Set up documentation for this project. Preserve existing documentation.
```

Personal skills stay local unless configured for cloud use. Cursor's **Settings → Agents → Context and Tools → Sync Skills for Cloud Agents** applies to `~/.cursor/skills/`, not `~/.agents/skills/`. For a shared cloud setup, use skills committed to the project. See the official [Cursor skills guide](https://cursor.com/docs/skills).

## Google Antigravity

For a new personal setup, use Antigravity. Google [announced the transition from Gemini CLI](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/) on May 19, 2026, with consumer request serving ending for the listed Gemini CLI and Code Assist offerings on June 18. That announcement has separate enterprise guidance; it does not mean every enterprise deployment stopped working.

For Antigravity App, CLI or IDE, copy both directories into either:

- Project: `.agents/skills/`
- User: `~/.gemini/config/skills/`

In the App or CLI, invoke `/living-documentation` for setup or `/documentation-impact` for maintenance and describe the task. In the CLI, run `/skills reload` if you added skills during a session. In the IDE, inspect active skills in its Customizations menu and request the desired skill by name. See the current [Antigravity skills guide](https://antigravity.google/docs/skills) and [Gemini CLI migration guide](https://antigravity.google/docs/cli/gcli-migration/).

## OpenCode

Copy both directories into either:

- Project: `.opencode/skills/` (or `.agents/skills/`)
- User: `~/.config/opencode/skills/` (or `~/.agents/skills/`)

Ask `Use the living-documentation skill to set up documentation for this project.` For a later change, ask `Use the documentation-impact skill to assess this change and update only affected sources.` OpenCode discovers the metadata and loads instructions through its `skill` tool. If a skill is missing, check its folder name, `SKILL.md` and skill permissions. See the official [OpenCode skills guide](https://opencode.ai/docs/skills/).

## Other agents and the standalone prompt

For another tool supporting the [Agent Skills specification](https://agentskills.io/specification), check its current discovery locations and invocation mechanism, then copy the complete skill directories there. `.agents/skills/` is shared by several tools, but is not a guaranteed universal location.

If skill loading is unavailable, open [`PROMPT.md`](../PROMPT.md), paste its full contents into the agent and state whether you want setup or focused maintenance. Give the agent access to the target project; if it cannot inspect or edit files, supply the relevant evidence and apply its proposed edits yourself.

## Verify and maintain the installation

Before asking for documentation changes, confirm that the tool can find both skill names and that `living-documentation/references/` contains both guides. Invoke the desired workflow explicitly on the target project and review the resulting changes. Installation and automatic invocation are different: this package does not add hooks or guarantee execution after every change.

Setup adds a documentation pointer to the project's `AGENTS.md` or existing `CLAUDE.md`. If your tool does not read that file, add a short pointer through its supported project-instruction mechanism, preserving existing instructions. The [standalone prompt](../PROMPT.md) remains available for manual use.

For updates and migration of older copies, follow [Update through your agent](#update-through-your-agent). To uninstall a managed installation, use Skills CLI's removal command for these two names at the chosen scope; for a manual installation, remove only these two installed skill directories. Generated project documentation is separate from the installed skills.

Verification includes a temporary project installation of both skills through Skills CLI 1.7.6 targeting Codex with `--copy`, a scoped project update and inspection of source tracking and packaged reference files on 2026-11-06. Tool-specific discovery, global installations and invocation have not been exercised in every listed tool. Recheck vendor guidance when an installed version differs or a path stops working.
