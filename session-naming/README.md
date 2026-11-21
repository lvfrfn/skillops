# Session Naming

Give the current session a searchable title based on its specific topic, useful scope, and intent. Use it once the task is clear, and revisit the title when new evidence materially clarifies the subject.

## Install

Install for Codex from your target project using the preferred `npx` method:

```bash
npx skills add lvfrfn/skillops --skill session-naming -a codex
```

Add `-g` for user-wide installation. See the [shared installation instructions](https://github.com/lvfrfn/skillops/blob/main/README.md#install-in-codex) for prerequisites and the manual fallback.

## Use

```text
$session-naming Name this session based on our investigation of DNS resolver timeouts in the API service.
```

A suitable title is `API service DNS resolver timeouts — investigate failures`. The skill preserves useful search terms and explicitly chosen titles, and avoids claiming a successful fix without evidence.

For routine activation, existing global `AGENTS.md` guidance can request this skill for each session. Verify activation in a newly started session; installation or implicit matching alone does not guarantee it runs every time.

## Requirements and limitations

The host must expose a native tool for changing the current session title. The instructions describe Codex's `mcp__codex_tui__set_thread_title` when available, but availability depends on the environment. Other agents require an equivalent native capability; compatibility has not been runtime-tested.

If the tool is unavailable or fails, the agent reports that limitation instead of editing backing session files. The skill applies only to the current session and does not rename historical sessions. It does not control the built-in auto-title generator or guarantee protection against later title replacement.

See [SKILL.md](SKILL.md) for the full instructions.
