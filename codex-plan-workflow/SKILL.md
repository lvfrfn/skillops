---
name: codex-plan-workflow
description: Guide Codex Plan mode through technical discussions, research, and decision-making before creating implementation plans. Default to discussion until the user requests or clearly confirms readiness to plan. Then produce a decision-complete execution handoff that preserves agreed decisions, rationale, context, constraints, and verification requirements for agents without conversation history. Use for DevOps, infrastructure, configuration, and software engineering tasks.
---

# Codex Plan Workflow

Complement Codex's native Plan mode rather than replacing it. Support technical discussion before planning, then produce a compact, independently executable handoff that preserves the context, constraints, and reasons behind the agreed approach. This applies especially to infrastructure, operations, configuration, and code changes.

## Discussion first; plan on readiness

- If the user explicitly requests an execution plan, enter plan-creation work immediately, but resolve consequential unknowns before finalizing it.
- Otherwise, **default to discussion and research**. Address the user's actual questions; do not ask whether they want a plan merely because Codex is in Plan mode.
- During discussion, inspect current behavior, investigate feasibility, compare alternatives, challenge assumptions, and explain tradeoffs. Illustrative implementation sequences are allowed; a finalized execution plan or `<proposed_plan>` is not.
- Do not infer permission to finalize a plan from sufficient information, the agent's confidence, or casual agreement with one technical point.
- Move to plan creation when the user requests it or clearly confirms both the intended approach and readiness to plan (for example, "let's turn this into a plan"). If readiness is unclear after the key decisions are settled, ask **one direct transition question**, then continue according to the answer.
- If the user reopens a decision during plan refinement, discuss that decision and update the whole plan only when the resulting approach is settled. Do not repeatedly ask about intent once it is established.

This controls the **deliverable**, not Codex permissions. Plan mode remains non-mutating; neither discussion nor a plan authorizes implementation, deployment, commits, or other changes.

## Prepare the handoff

1. **Ground the current state.** Inspect relevant repository files, configurations, runtime behavior, documentation, and available tools. Reuse findings already established in the conversation. Resolve discoverable facts through inspection before asking the user. Verify consequential external claims against authoritative sources when available; mark unsupported consequential claims **Unverified**.
2. **Resolve consequential decisions.** A decision is consequential if plausible alternatives change observable behavior, architecture, security, compatibility, operations, or an explicit requirement. Establish the chosen approach and why it was chosen. Preserve rejected alternatives only if their rationale prevents likely execution drift. Keep unapproved proposals distinct from accepted decisions; do not turn them into execution tasks.
3. **Close required gaps.** Ask a focused question when a required preference or fact cannot be discovered. Do not fabricate paths, identifiers, values, API contracts, approvals, or other required inputs. If a material decision remains unresolved, continue discussing rather than publishing a supposedly complete plan. Leave ordinary implementation choices to the executor.
4. **Specify only necessary work.** Cover the requested result and its direct dependencies. Prefer existing repository conventions and verification mechanisms. Do not add opportunistic refactors, speculative abstractions, duplicate validation, new dependencies, or unrelated cleanup. Specify algorithms, commands, or exact implementation details only where needed to preserve the agreed result or prevent a likely mistake.
5. **Review for independent execution.** Assume the executor cannot see the discussion. Check that the plan preserves the essential situation, decisions, reasons, constraints, invariants, dependencies, and acceptance conditions, without requiring it to infer consequential choices.

A handoff should be **complete in decisions, not exhaustive in instructions**. Do not make the executor rediscover agreed architectural choices, but do not prescribe routine code organization or every implementation step.

## Handoff content

Use the following as a flexible outline, not a mandatory five-section template. Merge or omit sections for small changes; include detail only when it changes execution or prevents a likely mistake. State shared constraints once instead of repeating them in every task.

### Outcome and boundaries

Define the goal, required deliverables, relevant scope and exclusions, and existing behavior that must remain unchanged. Capture security, compatibility, operational, and other consequential constraints. Describe actions needing separate authorization; the plan never grants permissions to the executor.

### Context and evidence

Provide the current state and essential findings, with relevant versions, deployment topology, configuration, identifiers, and artifact references. Use exact paths only when established and consequential; otherwise give a discoverable target (component, resource, or subsystem). Include sufficient facts directly in the plan so inaccessible links or the prior conversation are not required to understand it.

Distinguish material **observations** (confirmed in the environment), **documented facts** (source-backed), **inferences**, and **Unverified** claims when that distinction affects a decision. Avoid a source dump or labeling every trivial fact.

### Decisions and rationale

Record the final approach, its consequential tradeoffs, and the reasons it fits the requirements. Explain rejected or superseded approaches only where forgetting the reason could cause the executor to reverse an agreed decision. Do not include obsolete choices as parallel options.

### Execution specification

Organize work by dependencies, components, or expected behavior rather than mechanically listing files. For each meaningful work item, identify:

- Target and required inputs, including dependencies on earlier outputs.
- Required change or deliverable, with exact names, values, interfaces, and behavior where consequential.
- How successful completion can be established.

For infrastructure, specify relevant resources, ownership boundaries, configuration flows, operational failure modes, and rollout or rollback requirements when applicable. For code, specify agreed input/output contracts and compatibility requirements, not unnecessary helper functions or branches. For nonsoftware work, use the appropriate artifacts, roles, and acceptance criteria.

### Verification and blocking conditions

Separate checks already performed (and their evidence or limits) from checks the executor must run. Prefer existing checks and direct observation. **A completion check does not imply creating a new automated test.** Add tests only for meaningful behavior, contracts, regressions, or failure conditions; do not create tests for constants, static assignments, or behavior already guaranteed by an underlying library merely to fill the plan.

Identify material blockers: missing authorization, unavailable required input, contradictions with observed facts, or failures that prevent the agreed outcome. The executor should stop **affected dependent work** and report such blockers rather than silently redesigning the solution. Routine implementation issues may be resolved within the agreed approach; unrelated failures should be reported without automatically blocking independent work.

## Publish and refine

- In Codex Plan mode, use the native `<proposed_plan>` format **only** for a requested or clearly authorized, decision-complete implementation handoff. Never use it for research or exploratory discussion.
- Respect the user's requested output location and current mode permissions. Do not force files, worktrees, commits, subagents, TDD, or implementation.
- Keep the plan proportional to the task. Prefer a short precise handoff over repeated background, exhaustive path inventories, and tests that prove nothing.
- When revising an already published plan, return a **complete replacement** with superseded decisions removed from the tasks and checks. Do not publish fragments that require the executor to reconcile multiple versions.
- Do not add a redundant approval question when the next action has already been authorized.

Delegation is optional. If authorized subagents investigate independent questions, give them bounded assignments with evidence requirements; reconcile findings and preserve essential conclusions in the final handoff.
