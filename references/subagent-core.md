# Subagent Core

Use subagents for supervision, independent evidence gathering, falsification, re-anchoring, or bounded implementation only when they materially improve reliability.

## Ownership

The main agent owns:
- User Scope and phase;
- Control Authority and Evidence Authority;
- cumulative user corrections;
- action boundary;
- final reconciliation and acceptance.

Subagents do not reinterpret the overall task.

## Dispatch handoff

Resolve `SKILL_ROOT` from the actual installed `SKILL.md`. At Sentinel startup or replacement, pass the complete startup brief in `subagent-briefs.md`, including resolved canonical reference paths and current task evidence. On follow-up, supply relevant changed state and any unresolved blocker.

For custom-role children, also pass the canonical skill root, applicable reference paths, and the current evidence required by the assigned role. A role configuration or inherited conversation is not a substitute for this bootstrap. Missing or unavailable inputs are a review limitation, not a pass.

## Independence

For blind/adversarial review:
- dispatch with isolated/minimal context; do not transmit the main agent's preferred conclusions through inherited conversation;
- provide raw artifacts and acceptance criteria;
- withhold the main agent's conclusion, confidence, suspected defect, intended answer, and preferred verdict;
- ask what the evidence supports or what can falsify the claim;
- for before/after review, do not indicate preferred wording.

If the conclusion was disclosed, do not call the review blind.

## Hypothesis filter

Investigate a specialist finding only when it includes:
- exact claim/object;
- proposed failure mechanism;
- evidence pointer or reproducible search path;
- concrete verification/falsification path;
- material consequence if confirmed.

Vague concern does not create a new workstream.

## Review failure

These are failures, not clean passes:
- empty output;
- failed tool access;
- truncated output that misses requested scope;
- generic approval without evidence;
- refusal caused by an invalid brief;
- contaminated blind review.

A pass requires evidence that the requested scope was actually inspected.

## Reconciliation

The main agent validates every material finding against primary evidence.

- No majority vote.
- One concrete counterexample can defeat unsupported approvals.
- If agents disagree, inspect the disputed source directly.
- Do not average conflicting scientific claims.
- Preserve unresolved uncertainty instead of forcing consensus.

Update continuity state when an accepted finding changes authority, corrections, completed work, rejected paths, frontier, or completion conditions.

## Topology

Prefer a shallow structure:

```text
main agent
├── reliability sentinel
├── independent specialist reviewer
└── bounded worker, only if needed
```

Avoid recursive delegation by default. One artifact has one writer at a time unless a safe merge mechanism is explicitly available.
