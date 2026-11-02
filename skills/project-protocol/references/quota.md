# Codex quota protection (opt-in)

Use this reference when the user explicitly requests quota protection, for example
“请按照额度规则继续这个项目”, or the current project's authorized rule is enabled.
It is an operating agreement for Codex, not a platform-enforced interrupt or a new
quota monitor. Do not apply it to WorkBuddy or another provider's independent limits.

## Enablement and scope

Default: disabled. An absent rule or `enabled: false` does nothing. Installing or
upgrading this skill, quoting an example, reviewing history, or discussing the design
does not enable it. For a request without narrower scope, enable it for the current
project by adding this optional mapping to `.project/project.yaml`, preserving all
other fields. Confirm the effective scope and defaults briefly in the response.

```yaml
rules:
  quota:
    enabled: true
    threshold_remaining_percent: 14
    check_interval_minutes: 5
    wake_delay_minutes: 5
```

Only `enabled` is needed; omitted parameters use these defaults. Threshold is a
remaining percentage in [0, 100); intervals are positive minutes. Use explicit user
overrides and reconcile an existing project's maintained policy instead of keeping
conflicting copies. A missing project manifest requires authorized initialization;
otherwise apply only to the current task and report that persistence is unavailable.
If the user limits enablement to this task or session, keep that scope in its current
work; do not turn it into a project-wide flag. Scope-specific user instructions take
precedence. Do not infer that another account, project or provider is covered.

“关闭额度规则” disables it in the same scope (`enabled: false` for project scope).
Disablement does not resume business, remove existing schedules, or grant spending
authority. Reconcile any rule-owned pending wake with the user's current instruction;
cancel or pause it only when authorized. Never repurpose unrelated schedules.

## Observe actual capacity

At start or recovery, before and after a substantial batch or parallel dispatch, and
at safe checkpoints no more than `check_interval_minutes` apart during continuous
work, read the current signed-in Codex account's actual usage limits through the
available usage tool. Bound long operations and check between batches; a single
blocking operation may prevent a timely check, so do not promise a hard interrupt.

Treat Codex chats and Codex subagents on that account as sharing capacity. The
coordinator budgets for their combined consumption and leaves room to save and
integrate. Use each applicable model/account bucket and window, not an unrelated
healthy bucket. For tool values named `usedPercent`, remaining is
`max(0, min(100, 100 - usedPercent))`; null or missing is unknown. Read reset timestamps
and window lengths as returned, including both short and weekly limits where present.

All applicable limits strictly above the threshold and ordinary usage allowed:
continue authorized executable work immediately, including dependent next packages.
Knowing a future reset time is not a reason to wait. A reached limit, denied ordinary
usage or spend-control block also requires saving and stopping affected work.

If a needed reading or applicability is unknown, save current progress, stop new
quota-consuming batches, and make at most one bounded re-read. If still unavailable,
report the missing evidence; do not invent remaining capacity, a reset or a wake time.
Do not poll continuously or silently treat unknown as healthy. After an account
switch, read the new account; do not reuse the old account's reset assumptions.

## Warning and checkpoint

Any applicable remaining limit **at or below** the threshold starts wrap-up. Start no
new assignment or expensive batch. Save what is already useful and finish only a
small, safe checkpoint within the available capacity; do not spend the reserve trying
to finish the whole task. Ask active same-account Codex collaborators within the
assignment's authority to save and stop; shared capacity grants no control over
unrelated chats.
Record actual stopped, running or unknown writers separately from paused schedules.

Use the current Thread or existing engineering location to retain completed work,
exact files/versions, in-flight operations and writers, unchecked limits, and the next
action. A quota wait does not mean DONE, user-requested PAUSED, or executor Completion.
Do not fabricate an interrupted executor's return or add a second task registry.

## One recovery entry

When unfinished authorized work remains, explicit activation includes arranging a
quota-recovery wake for this scope if a real scheduling tool is available and allowed.
If unavailable or denied, keep the checkpoint and say that automatic recovery was
not configured. Do not work around the limitation with an unrelated automation.

Use the actual reset of the triggering window plus `wake_delay_minutes`. If several
applicable windows triggered, use the latest of their actual resets; an unknown reset
cannot be guessed. One coordinator reuses or reschedules one scoped recovery entry,
keeps its returned identity in current work, and reads back the saved configuration.
Use the tool's supported scheduling mechanism, not handwritten configuration. A saved
schedule is configuration evidence, not proof a future run will start or capacity
will have recovered.

Keep the wake prompt short: locate current project and Thread, re-read user authority,
enabled rule and actual current-account limits, then continue the saved next action
only if work remains and all gates allow it. If still in warning, use the new actual
reset for a single later wake. Do not run recurring empty quota checks. Do not recreate
an entry merely because its configuration result is uncertain; inspect that identity.

Completion, user stop/pause, disabled scope or whole-project closure prevents business
resumption. Retire rule-owned pending recovery when authorized; a late wake checks
these gates before doing work. A newly selected healthy account may continue after
verification without waiting for the old account. Quota changes never bypass user
verification limits. Purchases, paid capacity, reset vouchers or an account switch
require their own user instruction.
