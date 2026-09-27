# Codex Agent Runtime Check

Use this check once when reliability-critical multi-agent supervision starts, and again after a Codex/runtime change if effective subagent behavior becomes uncertain.

Configured agent files are desired policy, not proof of effective runtime behavior.

## Verify the standing Sentinel

Confirm, from runtime-exposed metadata or observable behavior when available:

- a child agent was actually created;
- the intended role/profile was selected if the runtime exposes role identity;
- effective model and reasoning effort match the expected policy or documented inheritance;
- the effective sandbox is read-only for reviewer roles;
- the child can be contacted again for later gates;
- the child did not silently fall back to a generic write-capable role.

Do not accept the child agent's self-description as proof of its effective configuration.

## If role/profile selection cannot be verified

Treat the child as a generic subagent.

Provide the necessary role constraints directly in the dispatch brief:
- read-only behavior;
- exact objective;
- required inputs;
- prohibited actions;
- evidence requirements;
- expected return shape.

Do not claim that a named custom agent configuration was applied.

## If read-only sandbox cannot be verified

Assume prompt-level read-only only.

Do not delegate actions whose safety depends on hard sandbox enforcement.
Keep reviewers away from destructive or write-required commands.

## If persistence/follow-up cannot be verified

Do not claim a resident Sentinel is active.

Re-establish supervision at the next mandatory gate using current User Scope, authorities, hard corrections, baseline, and compact continuity state.

## Failure semantics

Expected model/reasoning inheritance passes when it matches the documented policy and is supported by runtime evidence. Missing role metadata, unverified custom-role selection, unexpected or undocumented inheritance, sandbox mismatch, or lost follow-up capability are limitations of the requested setup, not proof that it was applied.

A verified generic child may perform the checks within its demonstrated capabilities; do not describe it as a verified custom role.

The main task may continue only with the capability actually verified.
