# Installation and tool setup

Status: current. Audience: developers and teams adding this method to their coding agent. Tool documentation and adoption sources were checked on **2026-11-06**. This guide covers installing this repository's instructions into an existing tool; use the linked vendor documentation to install the tool itself.

## Choose your tool

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

Install both if you want both workflows. Copy each **whole skill directory**, including the setup skill's `references/` directory. Copying only `SKILL.md` breaks its reference links. Keep the directory names unchanged.

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

In Codex, ask its built-in installer to install each skill:

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

Manual copies do not update when this repository changes. To update, compare a fresh download or clone with the installed directories, preserve any local customization, then refresh or restart the agent as required. To uninstall, remove only these two installed skill directories at the scope you chose, or use the tool's skill manager. Generated project documentation is separate from the installed skills.

Verification here is based on the linked vendor documentation and local package checks; the instructions have not been exercised in every listed tool. Recheck vendor guidance when an installed version differs or a path stops working.
