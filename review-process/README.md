# Review Process

Review or re-review pull requests and merge requests using scoped analysis, behavioral verification, and actionable findings. Use it for code, architecture, and documentation reviews where conclusions need evidence and clear verification limits.

## Use

Provide the PR/MR reference or local branch and comparison base, your concerns, and whether verification should remain static or include permitted execution:

```text
$review-process Review the current branch against main for retry regressions. Use static inspection only and report findings here.
```

For a follow-up:

```text
$review-process Re-review the updated branch against main and reassess the previous findings. Keep the review read-only.
```

Expect findings ordered by priority, tied to the reviewed revisions, with triggering conditions, impact, evidence, and recommended corrections. The conclusion distinguishes demonstrated defects, optional improvements, and missing verification.

## Requirements and boundaries

The agent needs access to the target revisions and relevant project contracts. Remote review and discussion handling depend on tools available in the host environment; this skill requires no particular integration and installs none.

Reviews are read-only by default. Editing, publishing comments, approving, pushing, or resolving discussions requires separate authorization. The workflow is agent-neutral; behavior outside Codex has not been runtime-tested.

See [SKILL.md](SKILL.md) for the full instructions.
