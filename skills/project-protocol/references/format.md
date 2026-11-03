# 0.7 file format

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
protocol: {name: project-protocol, version: '0.7'}
project: {id: stable-project-id, title: Project title, status: ACTIVE}
```

Project status is ACTIVE, PAUSED or CLOSED. Pausing/resuming follows user direction.
PROJECT contains stable purpose, scope and relevant project-wide constraints; actual
whole-project closure adds the result. Avoid duplicating live Thread progress here.

Optional rules belong in the manifest only when needed. `rules.quota.enabled` is a
Boolean, absent means false. Explicit project enablement writes true; explicit
disablement writes false. See [quota rules](quota.md) for parameters and scope.
Neither a copied example nor an old enabled snapshot grants current authority.

THREAD frontmatter requires `id`, `title`, `status` (ACTIVE, BLOCKED, DONE or STOPPED).
Its body supplies goal, current state, constraints, next action and finish conditions;
section names may vary. DONE records actual completion; BLOCKED names the missing
prerequisite; STOPPED records the user's stop decision. Keep the terminal result.

For multiple explicit requests, existing work can briefly map each to its output,
version, adoption and remaining gap. Keep important constraints' sources/scopes and
the user's selected baseline clear. These are body details, not mandatory new fields
or a separate registry; a small task needs no table.

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
Name inputs another writer could change and the accepted version to consume. If only
preparation or a trial is authorized before a dependency is ready, state its limits;
file existence or an upstream executor's DONE alone does not establish acceptance.

COMPLETION frontmatter identifies `handoff: TH-NNN/HO-NNN`, matching `project_id`, and
`outcome: DONE | PARTIAL | BLOCKED` for that assignment. Its body states actual work,
checks and limits, usable outputs and what remains. This is a receipt, not a second
current-state document. See the [Completion template](../templates/COMPLETION.md).
Save it beside the Handoff after execution, before Thread adopts the result.
Outcome describes the assignment, not acceptance of everything it inspected. A review
may be DONE with revisions required; PARTIAL may contain usable results. The
coordinator names the adopted outputs/versions and remaining issues in current work.
For corrections or continued execution, preserve the published return and link a new
return or supplement; update affected current plans without rewriting old findings.
Distinguish accepted deliverables from editable source and the last reproducible
baseline. Missing source or change evidence remains a stated version break.
When reusing checks, identify their input/version and covered scope; unchanged bytes do
not establish claims that were never checked. Changes to referenced objects,
dependencies or use conditions can also invalidate a previously checked statement
whose own file is unchanged. Recheck the affected conclusions within user limits,
not every unchanged artifact. Neither match counts nor all-PASS summaries substitute
for checking the specific claim and its supporting context.

IDs match their directories and are not reused, including after archival. Moving a
terminal Thread changes its location, not its outcome; retain its contents. Existing
0.3–0.6 metadata and headings may stay. Optional fields and sections can be omitted when
they add no information.
