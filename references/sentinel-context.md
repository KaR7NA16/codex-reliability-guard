# Reliability Sentinel — Context Health

Track one state:

- `HEALTHY`
- `SUSPECT`
- `DEGRADED`

## Weak signals

Repeated or clustered weak signals justify `SUSPECT`:

- asks for information already available in current authority;
- reopens a closed decision without new evidence;
- changes method/direction without a new evidential reason;
- refers vaguely to the user's objective or authority;
- re-explains/redefines the task instead of advancing it;
- rediscovers work already completed;
- process discussion or hedging grows while substantive progress falls;
- introduces unsupported details not grounded in current sources.

## Strong signals

Any can justify `DEGRADED`:

- current scope or authority cannot be stated consistently from primary sources;
- a completed/rejected/superseded instruction becomes active again;
- the agent treats existing authoritative information as missing and acts on that premise;
- contradictory task states are treated as simultaneously current;
- a recent user correction disappears from reasoning or action boundaries.

## Recovery

If `SUSPECT`, re-anchor from:

1. latest User Scope;
2. current Control Authority and Evidence Authority;
3. hard corrections and Do-Not-Reopen state;
4. actual execution state.

If `DEGRADED`, pause high-risk writes, destructive actions, status upgrades, and strong research claims until re-anchoring succeeds.

If self-audit remains unreliable, use a Cold-Context Reviewer with only:
- latest User Scope;
- current primary artifacts;
- relevant hard constraints;
- proposed next action.

Do not give it the main agent's long historical narrative unless needed.

## Cadence and continuity

For long tasks, lightweight context-health checks may supplement mandatory gates after a bounded run of meaningful actions. Choose the cadence by risk and context health; do not mechanically count trivial reads.

Preserve only decision-relevant state:
- context-health state;
- latest material gate;
- one active blocker if any;
- authority/baseline change;
- hard correction;
- unresolved release condition.

Do not create a separate sentinel journal.
