# 0.5 file format

Create files only as needed. Initialization needs a manifest, short PROJECT background
and an AGENTS skill pointer. THREADS.md is an optional locator, not another state store.
Starting templates: [Project](../templates/PROJECT.md), [Thread](../templates/THREAD.md)
and [AGENTS pointer](../templates/AGENTS.bootstrap.md).

```text
.project/project.yaml
.project/PROJECT.md
.project/threads/TH-NNN/THREAD.md
.project/threads/TH-NNN/handoffs/HO-NNN/HANDOFF.md
.project/threads/TH-NNN/handoffs/HO-NNN/COMPLETION.md   after execution
.project/archive/TH-NNN/                            entire ended Thread
```

## Identity and state

Use UTF-8 Markdown with YAML frontmatter for records, and this manifest shape:

```yaml
protocol: {name: project-protocol, version: '0.5'}
project: {id: stable-project-id, title: Project title, status: ACTIVE}
```

Project status is ACTIVE, PAUSED or CLOSED. Pausing/resuming follows user direction.
PROJECT contains stable purpose, scope and relevant project-wide constraints; actual
whole-project closure adds the result. Avoid duplicating live Thread progress here.

THREAD frontmatter requires `id`, `title`, `status` (ACTIVE, BLOCKED, DONE or STOPPED).
Its body supplies goal, current state, constraints, next action and finish conditions;
section names may vary. DONE records actual completion; BLOCKED names the missing
prerequisite; STOPPED records the user's stop decision. Keep the terminal result.

`owner`, `materials` and `latest_handoff` are optional conveniences. Owner identifies
the coordinating role. A handoff pointer locates an assignment, not every parallel
assignment; current work can name others when needed. Materials may be ordinary links
or existing `path`/`url` entries with a reason. Local references are project-relative.

## Handoff and return

HANDOFF frontmatter identifies `id: TH-NNN/HO-NNN` and `project_id`. Its body gives the
assignment, sufficient current context and constraints, needed materials, finish
conditions and return location. Date and material metadata are optional. See the
[Handoff template](../templates/HANDOFF.md).

HANDOFF.md is the assignment entry. Necessary images, configurations, logs or other
materials may be linked or included; existing stable engineering paths need no duplicate
package. Confirm that the receiving context can access what the assignment needs.

COMPLETION frontmatter identifies `handoff: TH-NNN/HO-NNN`, matching `project_id`, and
`outcome: DONE | PARTIAL | BLOCKED` for that assignment. Its body states actual work,
checks and limits, usable outputs and what remains. This is a receipt, not a second
current-state document. See the [Completion template](../templates/COMPLETION.md).
Save it beside the Handoff after execution, before Thread adopts the result.
When reusing checks, identify their input/version and covered scope; unchanged bytes do
not establish claims that were never checked.

IDs match their directories and are not reused, including after archival. Moving a
terminal Thread changes its location, not its outcome; retain its contents. Existing
0.3/0.4 metadata and headings may stay. Optional fields and sections can be omitted when
they add no information.
