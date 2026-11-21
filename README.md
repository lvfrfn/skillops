# skillops

A personal collection of agent skills for technical planning, code review, and searchable session names. The skills contain reusable instructions in `SKILL.md`; each folder's README explains when and how to use them.

Codex is the primary target. Other agents may use the instructions if they support loading `SKILL.md` files and provide the capabilities required by the skill. Installation paths and invocation syntax depend on the agent; compatibility with other agents has not been runtime-tested.

## Skills

| Skill | Purpose |
| --- | --- |
| [agent-plan-workflow](agent-plan-workflow/README.md) | Discuss technical decisions before producing an implementation handoff. |
| [review-process](review-process/README.md) | Review PRs and MRs with evidence, actionable findings, and explicit verification limits. |
| [session-naming](session-naming/README.md) | Give the current session a searchable title based on its actual topic and intent. |

## Install in Codex

### npx (preferred)

Requires Node.js 22.20 or later. Run from your target project to choose which skills to install for Codex:

```bash
npx skills add lvfrfn/skillops -a codex
```

Installation is project-local by default. To install one skill user-wide, add `--skill` and `-g`:

```bash
npx skills add lvfrfn/skillops --skill '<skill-name>' -a codex -g
```

Replace `<skill-name>` with a name from the table before running commands. See the [skills CLI documentation](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) for options and supported sources.

### Manual installation (fallback)

Clone the repository:

```bash
git clone https://github.com/lvfrfn/skillops.git
cd skillops
```

Copy the entire folder of each skill you want, replacing `<skill-name>` with its name from the table. Choose one destination to avoid duplicate installations. These commands assume the destination skill folder does not already exist.

#### User-wide

Available across your repositories:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R '<skill-name>' "$HOME/.agents/skills/"
```

#### Project-local

Available within the target repository. Run from the cloned `skillops` directory and replace `<project-path>` with the target repository root:

```bash
mkdir -p '<project-path>/.agents/skills'
cp -R '<skill-name>' '<project-path>/.agents/skills/'
```

The installed entrypoint should be `<destination>/<skill-name>/SKILL.md`. Cloning this repository alone does not place its skills in a Codex discovery directory.

### Verify discovery

Codex detects skill changes automatically. In the CLI or IDE extension, use `/skills` or type `$` to check discovery; restart Codex if the skill does not appear. See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills) for discovery locations and activation behavior.

## Use

Mention an installed skill explicitly in a Codex prompt, replacing `<skill-name>` with its name and `<task>` with your request:

```text
$<skill-name> <task>
```

Codex can also select a skill when a task matches its description. Installation alone does not guarantee activation for every task. Each skill README includes examples and specific requirements.

For another agent, use its documented skill installation and invocation mechanism. Review and planning guidance can be reused with compatible skill loading; session naming additionally requires a native tool for changing the current session title. These skills do not install tools or grant permissions.

## License

[MIT](LICENSE).
