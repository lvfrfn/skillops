# Agent Plan Workflow

Discuss and research technical decisions before producing a self-contained implementation plan. Use it for infrastructure, configuration, and software engineering work where the executor needs the agreed decisions, rationale, constraints, and verification criteria without the conversation history.

## Use

Start with discussion:

```text
$agent-plan-workflow Investigate how this service loads configuration and discuss options for hot reload. Do not finalize a plan yet.
```

When ready for a handoff:

```text
$agent-plan-workflow Turn the agreed hot-reload approach into an implementation plan, including constraints and verification criteria.
```

The skill defaults to discussion until you request or clearly confirm readiness to plan. The resulting handoff preserves the decisions and context needed by another engineer or agent. A plan does not authorize implementation.

## Compatibility

Previously named `codex-plan-workflow`. If you installed the old skill, replace that installed copy with `agent-plan-workflow` and update explicit invocations or agent guidance to use the new name. No alias is provided.

Follows the host agent's native mode restrictions and required plan format. In Codex Plan mode, finalized plans use `<proposed_plan>`; other agents use their required format or plain Markdown. Without a native planning mode, discussion and plan creation stay non-mutating. Other-agent behavior has not been runtime-tested.

See [SKILL.md](SKILL.md) for the full instructions.
