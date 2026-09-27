# Codex Reliability Guard

An instruction-based Codex skill that keeps long tasks aligned with user intent, corrections, evidence, and completion criteria.

Use it when an agent must preserve decisions across several phases, revise important artifacts, or recover from an earlier mistake. It guides the agent to check whether it is still solving the right task, using the right source, and making claims that the evidence supports.

The package contains **skill instructions, reference files, and optional custom-agent configuration templates**. Its behavior depends on the agent following those instructions and on the capabilities of the Codex environment. It does not install a background monitoring service or intercept tool calls.

- [When to use it](#when-to-use-it)
- [Quick start](#quick-start)
- [How supervision works](#how-supervision-works)
- [Optional custom-agent setup](#optional-custom-agent-setup)
- [Limits and overhead](#limits-and-overhead)
- [Design principles](#design-principles)
- [Files and further reading](#files-and-further-reading)
- [Feedback and license](#feedback-and-license)

## When to use it

Useful tasks include:

- **Repository refactoring, migration, or cleanup:** preserve existing work, action boundaries, and the behavior used to judge the change.
- **Document or visual revision:** preserve substantive content, attribution, and requested visible properties while improving the artifact.
- **Long or multi-agent work:** carry corrections through later phases and check the actual results produced by other agents.
- **Failure recovery or retrospective audits:** restore a supported state and distinguish current evidence from historical reports.
- **Research, manuscript, or proof work:** preserve assumptions, mechanisms, limitations, and evaluation baselines; check technical and novelty claims against suitable evidence.

Short, low-risk, single-step tasks can proceed without a standing Sentinel. Supervision is most useful when losing a decision or making an unsupported completion claim would materially affect the result.

## Quick start

### 1. Install the skill

Use a Codex environment that can discover local skills and read their supporting files. Download this repository using **Code → Download ZIP**, or clone it:

```bash
git clone https://github.com/KaR7NA16/codex-reliability-guard.git
```

Place the complete folder, named `codex-reliability-guard`, in **one** of these locations:

| Scope | Skill directory |
| --- | --- |
| One repository | `<repository>/.agents/skills/codex-reliability-guard/` |
| Your local user | `~/.agents/skills/codex-reliability-guard/` |
| Your local user on Windows | `%USERPROFILE%\.agents\skills\codex-reliability-guard\` |

The destination must contain `SKILL.md` directly:

```text
.agents/skills/codex-reliability-guard/
├── SKILL.md
├── README.md
├── LICENSE
├── agents/
├── references/
└── codex/
```

Keep the reference files with the skill. Copying only `SKILL.md` leaves its supporting instructions unavailable. Check for an existing installation before copying.

These locations follow the [official local skill documentation](https://learn.chatgpt.com/docs/build-skills). Codex detects newly installed skills; restart it if the skill does not appear. Installing the skill is separate from the [optional custom-agent setup](#optional-custom-agent-setup).

### 2. Confirm it can be loaded

Type `$` in a Codex prompt and look for `codex-reliability-guard`, or explicitly ask:

```text
Use $codex-reliability-guard. Read its SKILL.md and explain which
checks apply to a read-only repository review.
```

Confirm that Codex actually reads the installed `SKILL.md`. A response that merely repeats the skill name does not establish that it was loaded. If it is missing, check the folder layout and discovery location, then restart Codex.

### 3. Use it with a concrete task

The following is an illustrative prompt for a local refactor. Adapt the target and permitted actions to your repository:

```text
Use $codex-reliability-guard for this multi-stage task.

Goal: simplify the authentication module in the current repository
while preserving its public interface and authorization behavior.

Begin by inspecting the implementation, existing tests, and working
tree. You may then edit that module and its focused tests, and run
the relevant checks. Preserve unrelated local changes.
Do not commit, push, or deploy.

Use the original behavior as the evaluation baseline.
If I correct a requirement, apply it to the code, tests, and conclusions
that depend on it.

Finish with the changed behavior, validation evidence, and any remaining
uncertainty. Passing tests support only the behavior they actually cover.
```

At the start, the agent should identify the scope, allowed actions, baseline, and completion condition. For a task that qualifies for standing supervision, it should establish a Sentinel when usable subagent support exists, or explain the available fallback.

Check three things separately: the skill was loaded, a reviewer was actually created if applicable, and the reviewer inspected evidence at the relevant gates. These observations establish that the workflow ran; they do not prove that every error will be detected.

## How supervision works

The **Reliability Sentinel** is a reviewer that checks observable decisions, artifacts, and execution state. The main agent remains responsible for the task and for reconciling reviewer findings with primary evidence.

For long-running, multi-phase, repository-wide, hard-to-reverse, prior-failure-recovery, explicitly supervised, or other high-risk tasks, the skill requires a standing Sentinel by default **when usable subagent supervision exists**.

| Available capability | How the checks run | Boundary |
| --- | --- | --- |
| No usable subagents | The main agent performs the gate checks itself. | This is self-checking, not independent supervision. |
| Generic subagents | The main agent gives a child an explicit Sentinel brief and collects its findings. | A read-only instruction alone does not establish sandbox enforcement. |
| Verified custom agents | The main agent uses the configured role and checks its effective runtime settings. | Configuration files alone do not prove that the role or permissions were applied. |

The main agent re-contacts the Sentinel at these gates:

1. Start or resume.
2. Before a risky action.
3. After a correction or rollback.
4. Before a research or novelty claim.
5. Before a retrospective or provenance claim.
6. Before upgrading the reported status.
7. At a major phase boundary.
8. Before the final completion claim.

Long tasks may also use low-frequency checks between mandatory gates, with cadence chosen by risk and context health. Keep the same reviewer context when supported; otherwise, re-establish it from the current objective, evidence, corrections, and baseline. This is supervision through agent coordination, not an independently scheduled watcher with automatic access to every action.

The reviewer reports material issues with evidence and a condition for resolving them. It does not inspect hidden chain-of-thought. Separate specialist reviewers can challenge a technical claim, compare an original artifact with a revision, or test a novelty claim. Their findings require verification rather than a majority vote.

Reviewers remain read-only, including when a repair or reproduction would require writes. They can calculate, inspect sources, and perform read-only reproduction; the main agent or a separately authorized bounded worker performs the writing.

### Conditions and blocker release

A conditional pass states the actions or claims it permits, the prerequisites for the current gate, and any conditions belonging to later gates. Current prerequisites must be verified before the affected action proceeds. Required permissions, facts needed for a claim, and completion criteria cannot be deferred. Reporting partial progress does not complete the original objective.

The main agent closes a blocker through verified repair followed by review, or explicit reconciliation showing from primary evidence that the finding is false or inapplicable. Evidence-based rejection is the main agent's decision and must not be presented as reviewer agreement. It cannot override user permissions or another unresolved factual condition.

If a reviewer becomes unavailable, re-establish review where possible. If no usable replacement exists, perform the checks inline, state the limitation, and retain unresolved blockers. Missing output never counts as a pass; standing supervision resumes at later gates when support is restored. Quiet user-facing reporting still requires an internal gate result.

See [Sentinel checks](references/sentinel-core.md), [intervention rules](references/sentinel-enforcement.md), and [Codex coordination and fallback](references/codex-runtime.md).

## Optional custom-agent setup

The skill can use generic subagents without these templates. The optional kit supplies five custom roles: Reliability Sentinel, Cold-Context Reviewer, Semantic Preservation Reviewer, Novelty Adversary, and Technical Adversary. The [dispatch briefs](references/subagent-briefs.md) define Sentinel startup and specialist inputs.

When starting or replacing a Sentinel, the main agent passes the root of the selected installed skill, resolved paths to its Sentinel core and enforcement references, and the current task scope, gate, authorities, action boundary, baseline, corrections, completion condition, and primary evidence. The child reads those references before its first verdict. Copied templates and inherited context alone do not supply this handoff; keep the paths anchored to the actual skill installation.

### Install the templates

Choose either a user-level or project-level configuration:

| Scope | Configuration | Agent files |
| --- | --- | --- |
| User | `~/.codex/config.toml` | `~/.codex/agents/` |
| Project | `<repository>/.codex/config.toml` | `<repository>/.codex/agents/` |

1. Copy the files from [codex/agents](codex/agents/) into the chosen agent directory, checking for existing files with the same names.
2. Merge the relevant settings from [config.example.toml](codex/config.example.toml) into the chosen configuration. Preserve existing settings; combine existing TOML tables rather than adding duplicate tables.
3. Keep each `config_file` path relative to the configuration that declares it. For example, `./agents/reliability-sentinel.toml` must resolve to the copied file beside that configuration.
4. Restart Codex and verify the role can actually be selected and used. Project configuration also depends on the project being trusted.

The templates request high reasoning effort and read-only reviewer behavior. They do not pin a model. The example's global `default_subagent_reasoning_effort` setting affects other spawned agents in that configuration scope too; merge it only if that policy is intended.

See the official [custom-agent documentation](https://learn.chatgpt.com/docs/agent-configuration/subagents) and [configuration reference](https://learn.chatgpt.com/docs/config-file/config-reference) for the supported settings. This README does not specify a tested minimum Codex version or claim compatibility across every interface.

### Verify the effective behavior

Before relying on a custom reviewer, the main agent must check the evidence exposed by the runtime: a child was created, its intended role was applied where observable, its model and reasoning settings match the policy, its sandbox is appropriate, and it can be contacted at later gates.

Model and reasoning inheritance is valid when it matches the documented policy and is supported by runtime evidence. Unexpected, undocumented, or unverified settings require qualification.

Live parent-session permissions can affect child settings. A `sandbox_mode = "read-only"` entry is requested configuration, not proof of the effective permission boundary.

If role selection cannot be verified, use a generic child with an explicit role brief. If read-only enforcement cannot be verified, treat it as a prompt-level restriction and do not delegate actions whose safety depends on that enforcement. If follow-up is unavailable, re-establish review at subsequent gates rather than claiming a resident Sentinel remains active.

Use the [runtime verification reference](references/codex-runtime-check.md) for the complete checks.

## Limits and overhead

This is an instruction-based reliability workflow. It does not guarantee technical correctness, replace domain expertise or primary evidence, or create durable memory beyond the runtime's capabilities. The main agent must still follow the instructions, obtain relevant evidence, and handle reviewer findings.

Supervision adds model calls, context, and waiting time. The cost depends on task length, review frequency, model policy, and available tools; this package provides no measured overhead figures. Short tasks may use the core checks without a standing Sentinel. For qualifying tasks with usable subagents, keep the required supervision and load specialist references only when needed.

The design draws on recurring collaboration failures across software, research, documents, and visual work. The package does not include a controlled evaluation establishing error reduction or reduced human oversight. Those are design goals, not measured results presented here.

## Design principles

### Keep the task and its evidence distinct

Before substantive work, the agent establishes an **Active Contract**:

| Term | Plain-language meaning |
| --- | --- |
| User Scope | The objective and compatible requests the user currently wants handled. |
| Phase | Whether the agent is reviewing, editing, executing, restoring, or verifying. |
| Control Authority | The user's instructions, permission boundaries, hard constraints, and canonical project decisions. |
| Evidence Authority | The primary artifacts, direct observations, and verified state that determine factual claims. |
| Evaluation Baseline | The original version, behavior, sample, experiment, or question used to judge changes. |
| Completion Condition | Observable conditions that must hold before the task is complete. |
| Do-Not-Reopen | Completed, rejected, superseded, or forbidden routes that must stay closed unless the user reopens them. |

Only user instructions change the task scope. User control decisions remain in force when evidence conflicts with them; the agent reports that conflict instead of silently changing the objective. Existing unfinished objectives remain pending when compatible and not cancelled or suspended.

### Carry corrections through their consequences

A correction is a hard constraint until revoked. The agent identifies what became invalid and repairs or retracts dependent code, tests, artifacts, and conclusions within scope. Rollback takes priority: restore and verify the last supported state before continuing.

For long work, keep one compact continuity state. When context becomes `SUSPECT` or `DEGRADED`, re-anchor from current user instructions and primary artifacts. An independent Cold-Context Reviewer can help when the main agent's own state is unreliable. See [context recovery](references/sentinel-context.md).

### Match evidence to the claim

Evidence must be:

- **Type-matched:** it tests the property being claimed.
- **Discriminating:** it can distinguish success from a plausible failure.
- **Attributed:** its source, version, and relevant scope are identifiable.
- **Per-criterion:** each completion condition has its own support.

Passing tests cover tested behavior. Compilation does not establish proof correctness, export does not establish visual quality, and a failed search does not establish absence. Claims such as "all," "none," or "complete" require coverage of the bounded domain or an explicitly narrower conclusion.

### Preserve meaning and the original baseline

Revision must preserve substantive claims, assumptions, mechanisms, limitations, attribution, proof dependencies, prior-art distinctions, and requested visible properties. If the research object, estimator, sample, parameterization, experiment, or manuscript scope changes, identify the new object and its relation to the original before using it to judge the work.

Research retrieval and novelty evaluation are separate. A novelty claim needs the closest direct prior work, its limitation, a new mechanism or structural change, and a new consequence (**P–L–M–Δ**). Search adversarially for equivalent or closer work. Packaging, CI, dataset swaps, renaming, and generic model replacement alone do not establish scientific novelty. See [research retrieval](references/research-retrieval.md) and [novelty evaluation](references/novelty-evaluation.md).

### Act within scope and keep the workflow small

Check the target, current state, phase, and authorization before acting. Capabilities that can delete, publish, send externally, overwrite, or mutate persistent state need defined actors, triggers, scope, authorization, recovery, and protected defaults.

The workflow uses a shallow structure: main agent, Sentinel, and specialist reviewer or bounded worker when needed. Independent reviewers receive primary artifacts and acceptance criteria without the main agent's preferred conclusion. The skill does not require approval for every authorized step, extra process files, recursive supervisors, or a growing review journal.

### Recognize the failure families

| ID | Failure | Example |
| --- | --- | --- |
| F1 | Goal / Scope Drift | Solving an easier adjacent task. |
| F2 | Authority / State / Provenance Drift | Treating a superseded version as current. |
| F3 | Permission / Authorization / Execution Drift | Crossing the user's action boundary. |
| F4 | Evidence / Claim Mismatch | Promoting passing tests into a broader correctness claim. |
| F5 | Technical / Domain Correctness Failure | Relying on a faulty formula, algorithm, or validation assumption. |
| F6 | Semantic / Artifact / Baseline Fidelity Loss | Weakening content or judging a changed surrogate as the original. |
| F7 | Research / Retrieval / Novelty Failure | Missing direct prior work or mistaking packaging for novelty. |
| F8 | Correction / Recovery Failure | Fixing one artifact while dependent state stays stale. |
| F9 | Overengineering / Process Inflation | Producing scaffolding instead of the requested result. |

Confirmed or concretely evidenced failures pause the affected action or claim. The agent continues authorized inspection, validation, or repair that does not depend on the disputed result. Incomplete validation cannot support a stronger claim, but does not by itself stop all work. The [failure references](references/failure-taxonomy.md) explain the categories and response order.

## Files and further reading

[SKILL.md](SKILL.md) is the runtime entrypoint. References are loaded by function as needed. This README explains the package for readers; it does not replace the runtime instructions.

| Files | Purpose |
| --- | --- |
| [agents/openai.yaml](agents/openai.yaml) | Skill display metadata and default invocation prompt. |
| [codex/config.example.toml](codex/config.example.toml), [codex/agents](codex/agents/) | Optional Codex configuration and five reviewer templates. |
| [failure-taxonomy](references/failure-taxonomy.md), [failure-control](references/failure-control.md), [failure-quality](references/failure-quality.md) | Failure classification and corrective responses. |
| [sentinel-core](references/sentinel-core.md), [sentinel-context](references/sentinel-context.md), [sentinel-enforcement](references/sentinel-enforcement.md) | Supervision gates, context recovery, and intervention. |
| [subagent-core](references/subagent-core.md), [subagent-roles](references/subagent-roles.md), [subagent-briefs](references/subagent-briefs.md) | Delegation rules, Sentinel startup, specialist selection, and dispatch briefs. |
| [research-retrieval](references/research-retrieval.md), [novelty-evaluation](references/novelty-evaluation.md) | Frontier reconstruction and direct prior-art comparison. |
| [codex-runtime](references/codex-runtime.md), [codex-runtime-check](references/codex-runtime-check.md) | Codex coordination, effective-runtime checks, and fallback. |

## Feedback and license

Report problems or suggestions through [Issues](https://github.com/KaR7NA16/codex-reliability-guard/issues), or propose changes through a [Pull Request](https://github.com/KaR7NA16/codex-reliability-guard/pulls). For feedback, include the skill commit or version, the Codex environment, the task and expected behavior, and the observed failure. Include a minimal example or relevant output with private information removed.

This package is licensed under the [MIT License](LICENSE).
