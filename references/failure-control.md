# Failure Control

## F1 — Goal/Scope Drift

**Definition:** Work moves away from the latest user-originated scope.

**Signals**
- proof becomes status management;
- research becomes packaging or engineering;
- full-scope work becomes a local repair;
- a reference object replaces the actual target;
- process explanation replaces the requested answer;
- assistant- or sentinel-generated follow-up becomes the new objective;
- a closed decision is reopened without new user instruction or evidence.

**Response:** Re-establish User Scope, stop the substituted branch, and resume the requested task.

## F2 — Authority/State/Provenance Drift

**Definition:** Wrong or stale material is treated as current, authoritative, or correctly attributed.

**Signals**
- old manuscript/result replaces the current one;
- rejected routes re-enter the active chain;
- figure/file identity is guessed;
- summaries override primary artifacts;
- event/source/project/date identity is misassigned;
- missing local content is treated as proof the original source was empty;
- the agent asks for information already present in current authority;
- contradictory current states are carried simultaneously.

**Response:** Resolve Control Authority, Evidence Authority, object identity, source, chronology, and context health from primary evidence.

## F3 — Permission/Authorization/Execution Drift

**Definition:** The agent crosses the user's action boundary or designs mutation without authorization boundaries.

**Signals**
- analysis becomes modification;
- a plan request becomes execution;
- prohibited commands are run;
- destructive actions occur without recoverability;
- user-owned attribution/claims are changed without authority;
- protected paths are touched before dependency checks;
- delete/publish/external-send/persistent-mutation capability lacks actor, trigger, scope, authorization, or recovery rules.

**Response:** Stop the branch. Define missing authorization before implementation. Restore unauthorized changes when needed.

## F8 — Correction/Recovery Failure

**Definition:** A correction, rollback, invalidation, or re-anchor is only partially applied.

**Signals**
- only the user-pointed sentence is fixed;
- downstream artifacts/statuses remain inconsistent;
- rollback does not stop the old plan;
- forbidden content returns;
- pre-correction behavior is misreported as post-correction behavior;
- verbal withdrawal is not propagated into persistent materials;
- re-anchoring occurs verbally but the next action still follows stale state.

**Response:** Preserve chronology, trace dependents, repair/retract them, re-anchor from primary sources, and mark invalid routes Do-Not-Reopen where appropriate.

## F9 — Overengineering/Process Inflation

**Definition:** Scaffolding or supervision replaces the requested deliverable.

**Signals**
- new ledgers, schemas, phases, folders, wrappers, or managers appear without reducing uncertainty;
- cleanup creates another organizational system or nested copies;
- failure produces more governance instead of repair;
- each revision creates unnecessary backups, previews, reports, or packages;
- the sentinel emits a growing backlog instead of one actionable blocker;
- repeated warnings consume the task without new evidence;
- large raw logs/transcripts/arrays/histories/tool outputs are dumped into context when targeted inspection would suffice.

**Response:** Stop creating process artifacts or supervision noise. Return to the smallest action that directly advances the requested result.
