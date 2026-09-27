# Codex Subagent Runtime

Load when assessing Codex supervision capabilities, wiring subagents, or selecting a fallback when supervision is absent or unusable.

## Runtime verification

Before relying on a named custom agent for a mandatory reliability role, read `codex-runtime-check.md` and verify the effective runtime configuration when the runtime exposes enough evidence.

Configured TOML is policy, not proof that the child actually received the requested role, model/reasoning settings, sandbox, or persistence behavior.

## Standing sentinel

When usable subagent supervision exists, start one read-only Reliability Sentinel by default for long-running, multi-phase, repository-wide, destructive/hard-to-reverse, prior-failure-recovery, explicit continuous-supervision, or other high-risk work.

Resolve the actual installed skill root and dispatch the Sentinel with the canonical reference paths and current task inputs from `subagent-briefs.md`. Do not assume a copied custom-agent template or inherited context supplies the full contract.

Preserve the same sentinel identity/context when the runtime supports it. Re-contact it at mandatory gates; long tasks may also use low-frequency cadence checks.

Do not use the standing sentinel as the blind novelty, technical, semantic, or cold-context reviewer.

If persistent children are unavailable, re-establish a replacement from current User Scope, authorities, hard corrections, baseline, and compact continuity state. Do not reconstruct unresolved state from memory alone.

## Degraded-context fallback

When context health is `DEGRADED` or the main agent cannot reliably reconcile current state:
- pause high-risk writes and strong claims;
- invoke a Cold-Context Reviewer when available;
- provide only latest User Scope, current primary artifacts, relevant hard constraints, and proposed next action;
- withhold the main agent's long historical narrative and preferred resolution.

The cold-context result is an independent anchor, not automatic authority.

## Observation-first

Prefer actual runtime state over self-report:
- file diff / changed-file list;
- repository state;
- command/test output;
- rendered artifact;
- actual tool result;
- current authoritative file contents.

## Specialist reviewers

For blind/adversarial reviewers:
- prefer isolated/minimal context;
- provide raw artifacts and acceptance criteria;
- withhold the main conclusion/preferred verdict;
- treat empty, failed, truncated, or generic output as review failure;
- require concrete, checkable findings before opening a new workstream.

## Runtime truth

Do not assume a requested subagent profile, model, provider, sandbox, or reasoning setting was applied merely because it was requested.

Trust capabilities/metadata actually exposed by the runtime. If a specialized profile cannot be verified, treat the child as generic and include role constraints directly in its brief.

## Blocker discipline

Maintain at most one active sentinel blocker.

If the same blocker repeats without new evidence/state change, treat it as stalemate and switch to re-anchoring or cold-context review.

If direct child-to-main notification is unavailable, explicitly collect the child result before crossing a gated action.

Apply conditional-pass and blocker-release rules from `sentinel-enforcement.md`. If the Sentinel becomes unavailable, re-establish it from current evidence; if no usable replacement exists, use the inline fallback and retain any unresolved blocker. Lost contact is not evidence that a finding was false.

## Fallback

If subagent support is absent or unusable:
- apply the same gate checks inline;
- state the supervision limitation and retain unresolved factual or permission conditions;
- do not pretend an independent review occurred;
- do not treat missing reviewer output as a pass.
