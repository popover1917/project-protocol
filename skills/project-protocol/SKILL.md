---
name: project-protocol
description: Keep durable engineering work recoverable across agents and sessions; initialize project state, continue a Thread, or exchange an execution handoff. Ordinary queries and bounded edits need no protocol records.
metadata:
  short-description: Durable work with minimum context
---

# Project Protocol 0.5

Keep only what another agent needs to continue useful work. Project provides
background; Thread holds current work; Handoff and Completion carry an actual
assignment and its result. Use the [file format](references/format.md) when creating
or changing protocol records; templates are starting points, not required prose.

## Current work

Queries default to zero writes. Bounded edits change their artifacts. For work that
needs continuity, read the project manifest, relevant background and existing Thread;
reuse its goal. Create a Thread only for a distinct durable goal or an explicit
tracking request. Read referenced materials as needed, not the whole history.

Thread needs the goal, actual position, effective constraints, next step and finish
conditions. Update it when these change, not after every operation. Replace superseded
current instructions and link preserved history rather than layering overrides.
Keep information where it is maintained and reference it rather than copy it.
Decisions and verification belong in this work or its engineering materials. Consultations are
ordinary inputs; only authorized, adopted changes enter current state.

Retain a failed approach in existing work or engineering materials when it changes
how the next agent should continue; ordinary debugging needs no attempt log.

`.project` holds continuity state. Code, documents and results stay in appropriate
engineering paths; skill scratch stays in allowed temporary storage. Choose locations
by purpose, without creating unrelated workspaces for each skill.

## Execution transfer

Prepare a Handoff when another context needs an assignment: enough current context,
necessary materials, scope, finish conditions and where to return. Shared context
alone needs no packet. Preparing a packet does not establish takeover. Use one clear
entry and return location; link or include additional materials as needed, keeping
engineering originals and outputs where they are maintained.

The receiver checks the actual project, current files and existing return before
executing. Current engineering facts and user authority outrank snapshots. After
execution, save Completion with actual results, changes, checks or unverified limits,
and remaining work. The coordinating writer checks the result before updating Thread.
An existing return is reconciled rather than replayed; further transfer uses current
state. A missing return establishes neither execution nor success.

If an interrupted executor cannot return, a separate diagnosis grounded in evidence
can support authorized continuation. Preserve the original return or its absence, reconcile newer
work and resolve conflicting writers before resuming; do not fabricate the executor's
Completion.

One coordinating writer updates shared Thread state and assignments; each executor
may write its own Completion. Parallel scopes can be described in the Thread without
another task registry. Respect user verification limits: critical tests need explicit
authorization unless already covered, and stop at the authorized minimum closed loop.

## Finish and archive

An assignment finishing does not finish its Thread or Project. When a Thread's goal
is complete or the user stops it, retain its outcome and move its entire directory,
including handoffs, to `.project/archive/TH-NNN/`. Update maintained entry points to
the actual location; historical packets remain snapshots. BLOCKED work stays active.
Project closes only on explicit whole-project closure.

## Version changes

Read the instance's declared version before mutation. Installation does not migrate
projects. For an authorized upgrade, retain a recoverable old snapshot, preserve useful
identity and work, then declare the new version. 0.3 and 0.4 records can keep their content
in 0.5; archive ended Threads without rewriting old receipts. For other formats, preserve
data and resolve conversion before protocol mutation; engineering work may continue
within its own authority. No automatic migration of other projects.

## Optional integration

For Codex–WorkBuddy scheduled collaboration, read the [WorkBuddy reference](references/workbuddy.md)
only when that mode is in scope.
