---
name: project-protocol
description: Keep durable engineering work recoverable across agents and sessions; initialize project state, continue a Thread, or exchange an execution handoff. Apply optional Codex quota rules on explicit request (请按照额度规则). Ordinary queries and bounded edits need no protocol records.
metadata:
  short-description: Durable work with minimum context
---

# Project Protocol 0.7

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
For work with several explicit requests, connect them to the actual outputs/versions,
adoption and remaining gaps in existing work or engineering plans. An aggregate DONE
does not cover a missing requested item; a simple task needs no coverage matrix.
For constraints that change direction or block execution, retain their source and
scope: user requirement, external requirement, project choice, tool limitation or
unknown fact. Recommendations and examples do not create new mandatory gates.

Keep information where it is maintained and reference it rather than copy it.
Identify material roles and current baselines: requirements, reference, editable
source and accepted deliverable are not interchangeable. Carry the user's selected
version and allowed changes into downstream work; editing convenience or agent
preference does not authorize replacement. If a real conflict prevents that choice,
surface the conflict; ordinary authorized implementation choices remain autonomous.
Maintain usable entries and old-to-new location mappings when moving materials.
Decisions and verification belong in current work or engineering materials. Keep
internal continuity/checking detail there; user-facing deliverables should serve
their audience and retain relevant limits without repeating the internal protocol.

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
engineering originals and outputs where they are maintained. Before parallel work,
consider writes affecting another task's reads and shared meaning, even when output
directories differ. Downstream production consumes an accepted fixed input; before
that is ready, authorize only useful preparation or trial work with its reuse and
rework limits clear. This does not require fixed stages or another dependency registry.

The receiver checks the actual project, current files and existing return before
executing. Current engineering facts and user authority outrank snapshots. A closed
project or user stop is not reopened by an old ACTIVE marker, recurring prompt or
retrospective suggestion. After execution, save Completion with actual results,
changes, checks or unverified limits, and remaining work. The coordinating writer
checks the result before updating Thread.
An existing return is reconciled rather than replayed; further transfer uses current
state. A missing return establishes neither execution nor success.

The coordinator remains responsible for actual start, return, adoption, integration
and usable delivery within continuing authorization. Writing an assignment is not
starting it, and finishing one bounded package is not a new approval gate. Adopt
specific returned outputs and versions, including usable parts of PARTIAL; completing
a review can legitimately conclude that the reviewed artifact needs revision. Keep
execution outcome, artifact acceptance and outstanding configuration distinct.
Preserve published returns when correcting or continuing them, linking the new return
or supplement to the prior one rather than silently replacing its history.

Before adopting a finding, locate its actual object and context; distinguish a
verified defect, a suggestion and an unchecked inference. Automated matches and tool
alerts need that interpretation before becoming repair assignments. If an adopted
finding is corrected or withdrawn, reconcile affected current tasks and conclusions,
preserving valid later work and the correction trail. Do not add routine tests or
approval steps merely to establish this relationship.

Separate file identity and build checks from content, visual or task-specific
acceptance; state the version and scope each conclusion covers. Preserve an external
version break when editable source or change evidence is missing rather than invent
lineage. Apply corrections and rechecks to their actual impact rather than restarting
the whole workflow because of a result label.

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
Project closes only on explicit whole-project closure. Closure does not retroactively
complete unexecuted assignments; retain their actual state and missing returns.

## Version changes

Read the instance's declared version before mutation. Installation does not migrate
projects. For an authorized upgrade, retain a recoverable old snapshot, preserve useful
identity and work, then declare the new version. 0.3–0.6 records can keep their content
in 0.7; archive ended Threads without rewriting old receipts. For other formats, preserve
data and resolve conversion before protocol mutation; engineering work may continue
within its own authority. No automatic migration of other projects.

## Optional integration

Quota protection is off unless the user explicitly enables it. For “请按照额度规则……”
or an enabled `rules.quota` in the project manifest, read the [quota reference](references/quota.md).
It defines the opt-in, saving and recovery behavior; installation or discussing the
rule does not enable it or create a schedule.

For Codex–WorkBuddy scheduled collaboration, read the [WorkBuddy reference](references/workbuddy.md)
only when that mode is in scope.
