---
name: codex-reliability-guard
description: Guard long-running or high-risk Codex tasks against scope/state drift, lost corrections, unsupported completion claims, and semantic regression. Use when work spans multiple phases, changes important artifacts, recovers from prior failures, or requires continuous supervision.
license: MIT
---

# Codex Reliability Guard

Keep the user's objective, authority, evidence, evaluation baseline, and deliverable stable while work proceeds. This is a reliability guard, not a project-management framework. Do not create extra ledgers, plans, schemas, folders, or process artifacts unless the requested task itself requires them.

## 1. Active contract

Before substantive action, determine:

- **User Scope** — active objective, additive requests, suspended/superseded requests.
- **Phase** — analysis, review, editing, execution, rollback, verification, audit, or another current phase.
- **Control Authority** — current user objective, permission boundary, hard constraints, canonical project decisions.
- **Evidence Authority** — primary artifacts, direct observations, verified runtime/repository/data state, and authoritative sources that determine factual claims.
- **Evaluation Baseline** — the original object, version, question, estimator, sample, experiment, or manuscript used to judge change.
- **Completion Condition** — observable conditions required for actual completion.
- **Do-Not-Reopen** — completed, rejected, superseded, or explicitly forbidden routes.

Only user-originated instructions can create, change, suspend, supersede, or reopen User Scope. The latest user message controls the immediate turn. Earlier unfinished objectives remain pending only when not cancelled/suspended and still compatible.

Do not collapse Control Authority and Evidence Authority. User instructions govern what to do; primary evidence governs what is factually true. If they appear to conflict, preserve the user's control decision and report the evidential conflict instead of silently choosing one.

If the user names an inspectable artifact that materially determines the answer, inspect it before inferring its contents or asking the user to restate information already available.

When long-task state loss is plausible, maintain one compact continuity state only: current scope, phase, authorities, baseline, hard corrections, completed work, Do-Not-Reopen paths, current frontier, next action, and completion condition. It is navigation, never authority.

## 2. Load only the references needed

Use progressive disclosure.

- Read `references/failure-taxonomy.md` to classify a detected failure.
- Read `references/failure-control.md` for F1/F2/F3/F8/F9.
- Read `references/failure-quality.md` for F4/F5/F6/F7.
- Read `references/sentinel-core.md` when establishing or using standing supervision.
- Read `references/sentinel-context.md` for long-context, resume, compaction, or degraded-context recovery.
- Read `references/sentinel-enforcement.md` before applying a conditional verdict, clearing a blocker, or crossing a disputed gate.
- Read `references/subagent-core.md` before reliability-critical delegation.
- Read `references/subagent-roles.md` to choose a specialist role.
- Read `references/subagent-briefs.md` when starting/replacing a Sentinel or dispatching a specialist.
- Read `references/research-retrieval.md` for broad field research or coverage claims.
- Read `references/novelty-evaluation.md` for novelty or contribution claims.
- Read `references/codex-runtime.md` for Codex supervision capability assessment, subagent wiring, or unavailable-supervision fallback.
- Read `references/codex-runtime-check.md` when custom-agent role, model/reasoning, sandbox, or persistence must be verified.

## 3. Standing Reliability Sentinel

When usable subagent supervision exists, run one read-only Reliability Sentinel by default for tasks that are long-running, multi-phase, repository-wide, destructive/hard-to-reverse, recovering from a prior failure, explicitly under continuous supervision, or otherwise high-risk.

Short, low-risk, single-step tasks may proceed without a standing sentinel. The main agent may not waive required supervision merely because it believes the task is going well.

If subagent supervision is absent or unusable, perform the same gate checks inline and state the limitation. Do not claim independent review or treat missing reviewer output as a pass.

Before dispatch, resolve the actual skill root and pass the Sentinel the canonical reference paths, current gate, scope, authorities, action boundary, baseline, hard corrections, completion condition, and primary evidence. Use the Sentinel brief; do not rely on inherited context to supply its operating rules.

The sentinel audits observable decisions, actual artifacts, and execution state. It does not claim access to hidden chain-of-thought.

Mandatory gates:

1. START / RESUME
2. PRE-RISK ACTION
3. POST-CORRECTION / ROLLBACK
4. RESEARCH OR NOVELTY CLAIM
5. RETROSPECTIVE / PROVENANCE CLAIM
6. STATUS UPGRADE
7. MAJOR PHASE BOUNDARY
8. FINAL

Long tasks may also use low-frequency cadence checks after a bounded run of meaningful actions. Supervision is report-by-exception, not constant chatter.

A conditional verdict releases only its stated action/claim scope after all current-gate prerequisites are satisfied. Close blockers through verified repair or explicit reconciliation against primary evidence, following `references/sentinel-enforcement.md`; an unresolved factual or permission condition still blocks its affected action. Gate results must be collected even when user-facing supervision is quiet.

## 4. Core invariants

### Corrections propagate

A user correction is a hard constraint unless explicitly revoked. Identify what became invalid, trace its direct dependents, repair/retract them within scope, mark invalid routes Do-Not-Reopen when appropriate, then continue the original task.

Rollback/revert/restore preempts the prior plan. Restore and verify the last supported state before resuming.

### Evidence matches claim

Strong claims require evidence that is:
- **Type-matched**
- **Discriminating**
- **Attributed**
- **Per-criterion**

Compilation is not proof correctness. Passing tests cover only tested behavior. Export success is not artifact quality. Failure to find something is not proof of absence. Small samples support only scoped conclusions.

Universal or absence claims such as `all`, `none`, `no remaining`, `full`, or `comprehensive` require coverage of the actual bounded domain or an explicitly narrowed claim.

### Preserve semantics and baseline

Do not improve presentation by deleting or weakening claims, novelty, assumptions, mechanisms, prior-art distinctions, limitations, proof dependencies, attribution, or requested visible properties.

Do not judge the original work through a narrowed surrogate created during editing. If the research object, estimator, sample, parameterization, experiment, figure responsibility, or manuscript scope changes, name the new object and establish its relation to the original first.

### Permission and execution

Before modifying, running, delegating, or designing a state-changing capability, verify target, current state, phase, and authorization.

Reviewers remain read-only. Direct calculation and read-only reproduction are allowed; authorized rewrites or reproductions requiring writes belong to the main agent or a bounded worker.

Capabilities that can delete, publish, send externally, overwrite, mutate persistent state, or cause hard-to-reverse effects must define actor, trigger, scope, authorization, recovery, and protected defaults before implementation.

Avoid large raw-output dumps when targeted inspection or summarized evidence is enough.

## 5. Failure response

For a confirmed or concretely evidenced F1-F9 failure, pause the affected action or claim and follow its corrective response. Continue authorized inspection, validation, or repair that does not depend on the disputed result. Incomplete validation alone does not require stopping all work, but it cannot support a stronger claim. Validate the task frame before trusting object-level work:

1. permission/authorization;
2. authority/object/provenance/context identity;
3. correction/rollback propagation;
4. active user scope;
5. technical correctness;
6. semantic/baseline fidelity;
7. evidence/claim strength;
8. research/novelty quality;
9. process inflation.

If context health is degraded, re-anchor before relying on lower-priority self-assessment.

Do not respond to failure by inventing another management layer.

## 6. Completion gate

Before declaring completion, verify internally:

1. latest user-originated scope is still being solved;
2. context health is sufficient;
3. phase and authorities are correct;
4. corrections/rollback propagated;
5. actions stayed within authorization;
6. strong claims have matching evidence and coverage;
7. universal/absence claims cover their bounded domain;
8. substantive content and evaluation baseline survived;
9. novelty claims have adequate direct-prior-art support;
10. the actual final artifact/result was inspected;
11. subagent findings were reconciled against primary evidence;
12. recommendations, rankings, numbers, statuses, and conclusions are internally consistent;
13. deliverable format, count, destination/path, and packaging match the user's request;
14. the user's completion condition is actually satisfied.

If any check fails, continue the original task or state the precise remaining blocker. Do not create a process artifact as a substitute.
