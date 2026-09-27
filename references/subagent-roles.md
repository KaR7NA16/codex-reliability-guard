# Subagent Roles

Choose only roles relevant to the task.

## Reliability Sentinel
**Purpose:** standing, context-aware supervision.  
**Checks:** User Scope, context health, authorities, corrections, evidence, risky actions, completion claims.  
**Must not:** act as a blind reviewer or take over project management.

## Cold-Context Reviewer
**Purpose:** independent re-anchoring when context health is degraded.  
**Input:** latest User Scope, current primary artifacts, hard constraints, proposed next action.  
**Must not:** inherit the main agent's long historical narrative or preferred resolution unless required.  
**Return:** current task, authorities, applicable constraints, whether the proposed action follows, unresolved conflicts.

## State/Authority Auditor
**Purpose:** resolve current task pointer and authority.  
**Return:** active task/phase, authoritative objects, stale/historical/superseded items, unresolved identity/version/source/time conflicts, exact evidence.  
**Must not:** propose a workflow.

## Semantic Preservation Reviewer
**Purpose:** detect substantive or baseline regressions between original and revision.  
**Check:** claims, novelty, assumptions, scope, mechanisms, prior-art delta, limitations, attribution, research-object continuity, requested visible properties.

## Evidence/Completion Auditor
**Purpose:** determine what the evidence actually proves.  
**Check:** type match, discrimination, attribution, per-criterion support, proxy/claim mismatch, coverage, universal/absence claims, completion conditions.

## Novelty Adversary
**Purpose:** try to invalidate novelty.  
**Search for:** closer prior art, equivalent formulations, older terminology, hidden assumptions, mechanism-level equivalents in adjacent fields.

## Technical Adversary
**Purpose:** falsify the controlling mathematical, algorithmic, data, experiment, or implementation claim.  
**Return:** smallest counterexample/failing path or exact checked scope if none is found.

## Bounded Worker
**Purpose:** perform one explicitly delegated implementation result.  
**Needs:** exact objective, exclusive owned artifacts, protected artifacts, dependencies, acceptance criteria.  
**Must not:** decide project authority, redefine scope, or mark the parent task complete.
