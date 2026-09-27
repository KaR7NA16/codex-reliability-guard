# Failure Taxonomy

Use this file only to classify a failure and route to the relevant detailed reference.

## Control and state failures

Read `failure-control.md` for:

- **F1 — Goal/Scope Drift**: work moves to an adjacent, easier, narrower, or assistant-generated task.
- **F2 — Authority/State/Provenance Drift**: stale, historical, wrong-version, wrong-object, wrong-source, wrong-time, or context-degraded material is treated as current or correctly attributed.
- **F3 — Permission/Authorization/Execution Drift**: the agent crosses the user's action boundary or designs a state-changing capability without an authorization model.
- **F8 — Correction/Recovery Failure**: correction or rollback is applied locally while dependent state remains stale, chronology is misread, or a rejected path returns.
- **F9 — Overengineering/Process Inflation**: scaffolding, supervision chatter, file proliferation, or workflow growth replaces progress on the requested deliverable.

## Quality and evidence failures

Read `failure-quality.md` for:

- **F4 — Evidence/Claim Mismatch**: evidence is promoted beyond what it supports in type, discrimination, attribution, coverage, quantifier scope, or completion.
- **F5 — Technical/Domain Correctness Failure**: a controlling formula, algorithm, implementation, dataset, experiment, proof step, or validation assumption is wrong or insufficiently checked.
- **F6 — Semantic/Artifact/Baseline Fidelity Loss**: editing or transformation weakens substantive content, requested artifact quality, or the identity of the research object used for evaluation.
- **F7 — Research/Retrieval/Novelty Failure**: weak retrieval or poor frontier discrimination produces weak research conclusions, poor recommendations, or false novelty.

## Causal order

Repair the earliest causal failure first:

1. F3 permission/authorization;
2. F2 authority/object/provenance/context identity;
3. F8 correction/rollback/recovery;
4. F1 active user scope;
5. F5 technical correctness;
6. F6 semantic/artifact/baseline fidelity;
7. F4 evidence/claim strength and coverage;
8. F7 research/novelty quality;
9. F9 process inflation.

If context health is degraded, re-anchor before relying on lower-priority self-assessment.
