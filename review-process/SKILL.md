---
name: review-process
description: Review or re-review merge requests and pull requests across projects using scoped analysis, behavioral verification, regression provenance, actionable findings, and verified discussion handling.
---

# Review Process

Use this baseline for MR and PR reviews of code, architecture, and documentation. Apply it alongside applicable project instructions and available specialized skills. Current user instructions govern scope and authorization. Keep project identifiers, tool commands, technology checks, and local severity conventions in project guidance; this skill requires no particular tool and grants no permissions.

## Scope and permissions

- **Establish the review contract.** Identify the target MR, intended outcome, explicit concerns, included components, exclusions, verification mode, and requested deliverable. Inspect available sources first. If required information remains missing, ask one direct question; do not invent assumptions. Continue work that does not depend on the answer.
- **Keep reviews read-only by default.** A review request does not authorize edits, commits, pushes, approvals, comments, or resolving discussions. Git operations, local execution, and installations follow existing permissions. Preserve authorization already granted without broadening it or repeatedly requesting it.
- **Review exact revisions.** Record the source head and comparison base. Confirm local files and other revision-dependent evidence match the reviewed revision before relying on them.
- **Read governing contracts.** Consult applicable agent instructions, project guidelines, issue requirements, architecture decisions, and relevant documentation. Identify contradictions rather than silently selecting a convenient interpretation.
- **Answer the stated question first.** Determine whether the change achieves the requested behavior. Assess explicit architectural concerns even when the code compiles and tests pass; distinguish a demonstrated design problem from an equally valid alternative.
- **Control dependency scope.** Inspect surrounding code and consumers needed for the agreed review. For named sibling MRs, trace their shared contract and retain separate conclusions. Expand scope only when authorized; otherwise identify the external evidence gap.

## Behavior and completeness

- **Trace effective behavior.** Follow inputs through transformations, defaults, overrides, outputs, and actual consumers. Syntax validity and a plausible implementation do not establish correctness.
- **Use realistic conditions.** Establish supported versions, active consumers, environment differences, and relevant configurations before judging behavior. Do not invent usage scenarios to justify a finding.
- **Inspect the complete relevant change.** Include additions, deletions, moves, tests, documentation, and integration points. Confirm removed behavior or context was actually lost before reporting it. Explain material coverage limits, including excluded or unavailable artifacts.
- **Prove MR causality.** Report defects introduced, worsened, or made reachable by the change. Compare the exact base and head to establish that relationship. Separate unrelated baseline defects from MR findings.
- **Assess meaningful failure cases.** Follow changed behavior into relevant boundaries, invalid inputs, failure handling, lifecycle transitions, and interactions. Derive cases from actual contracts and risks rather than applying an exhaustive generic checklist.

## Design and verification

- **Challenge complexity with concrete reasoning.** Prefer DRY and KISS. Assess unnecessary configuration knobs, duplicate ownership, speculative abstractions, and obsolete paths within scope. Explain the maintenance or correctness cost and a simpler viable alternative. Preserve complexity needed for isolation or correctness.
- **Make compatibility contextual.** Establish existing consumers and accepted breaking changes. Require a migration when agreed compatibility cannot be preserved. Avoid compatibility scaffolding for explicitly unused contracts.
- **Respect staged delivery.** Distinguish implementation defects from acknowledged preparation tasks and deferred phases. Treat deferred work as a blocker only when it prevents the agreed stage from meeting its acceptance criteria. Respect explicitly accepted interim conditions.
- **Evaluate tests as code.** Check whether assertions detect the relevant broken behavior. Inspect mocks, fixtures, omitted branches, and integration boundaries. Passing checks prove only what they exercise; recommend additional tests for meaningful gaps rather than constants or implementation mirroring.
- **Respect execution boundaries.** Static review stays static. Run targeted checks when authorized; inspect scripts and delegated subprocesses for side effects first. Prefer existing tools and evidence. Do not execute operational or destructive actions merely to verify a claim.
- **Verify consequential claims.** Use current implementation, direct observations, and official documentation appropriate to the relevant version. Corroborate author statements, previous reviews, and agent claims. Agreement between reviewers is not proof.
- **Separate uncertainty from defects.** Unavailable access, tools, or runtime evidence means **Unverified**, not a confirmed defect. State what evidence would resolve the gap and continue independent review. Qualify the verdict when essential evidence remains unavailable; do not claim universal correctness from limited checks.
- **Review documentation as user-facing behavior.** Check accuracy, essential context, examples, references, and agreement with implementation. Preserve authoritative ownership and useful explanations of why. Check whether removed context remains accessible through a suitable reference. Request additional explanation, restructuring, or diagrams only to resolve a concrete comprehension problem.

## Findings and conclusions

- **Make findings actionable.** State the exact location, triggering condition, expected versus actual behavior, impact, evidence, MR causality, and smallest suitable correction. Critique the implementation rather than the person. Do not present an unverified correction as a proven fix.
- **Calibrate priority and blocking status.** Use project severity conventions when provided; otherwise explain priority through demonstrated impact. Distinguish required corrections, optional improvements, and verification gaps. Personal preferences and cosmetic polish should not block an acceptable change.
- **Deduplicate findings.** Group repeated symptoms of the same root cause. Read existing discussions before adding comments. Require no finding quota; prefer supported findings over speculative volume.
- **Finish with a bounded conclusion.** Report actionable findings first, ordered by priority, followed by reviewed revisions, relevant checks, material verification gaps, and a direct verdict for each MR. Use **Needs changes** for demonstrated required corrections, **Acceptable with suggestions** for optional improvements only, or **No actionable issues found within reviewed scope** when appropriate. If missing essential evidence prevents a verdict, say so directly.

Use this compact format for each finding; combine fields when that improves clarity:

```text
[Priority] Specific title
Location:
Trigger and expected behavior:
Actual behavior and impact:
Evidence and MR causality:
Recommended correction:
Blocking or optional:
```

## Re-review and discussions

- **Re-review fresh evidence.** Refresh current revisions through permitted tools. Inspect the new delta, revisit affected behavior and contracts, and reassess previous findings. Classify each as fixed, remaining, superseded, or unverified. An open or resolved thread does not establish the current behavior.
- **Handle discussions precisely when authorized.** Anchor supported findings at relevant changed lines where suitable. Reuse original discussions rather than duplicating them. Verify posted content, location, revision, and intended discussion state. Resolve only after confirming the fix. For authorized implementation and replies, publish changes before replying. After an ambiguous write result, read back the state before retrying to avoid duplicate comments; if verification is unavailable, report that limitation.

## Sources

These sources support the review principles; they do not replace project contracts or user instructions:

- [Google: The Standard of Code Review](https://google.github.io/eng-practices/review/reviewer/standard.html) — evidence, proportionality, and acceptable alternatives.
- [Google: What to Look For in a Code Review](https://google.github.io/eng-practices/review/reviewer/looking-for.html) — design, behavior, complexity, tests, documentation, and context.
- [Google: How to Write Code Review Comments](https://google.github.io/eng-practices/review/reviewer/comments.html) — actionable reasoning and clear comment intent.
- [GitHub: Copilot Agents Application Card](https://docs.github.com/en/copilot/responsible-use/agents) — false positives, missed defects, and review limitations.
