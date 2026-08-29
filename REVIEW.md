# Weekly review

Memory for the weekly review task. It reads a week of runs and edits the rules.
It does not triage. It reads the inbox but never changes it.

## What this system is for

The inbox is an action queue, not an archive. Gmail search is the filing system,
so archiving costs attention, not data — anything archived is one search away,
forever.

It exists because the inbox fills faster than Miles clears it. A 200-thread
backlog of month-old dead reminders is the state it was built to end. Every
weekday at 7am the triage reads the inbox, archives what is dead, and hands him
a brief covering only what is live: people waiting on a reply, and actions with
a deadline still ahead.

**The goal is not an empty inbox.** The goal is that whatever is still in the
inbox is exactly what he still has to do, so the inbox can be trusted as the
list. An inbox holding forty dead reminders is not a list, it is a pile, and a
pile is what this replaced.

Your job is to keep that true as the mail changes. The rules were written
against the inbox as it was in August. Senders change, subscriptions come and
go, and a judgement that was right then can be wrong in November.

## The two failure modes

1. **Wrong archive** — something he wanted was taken out. Expensive: he has to
   notice it is missing before he can go looking for it.
2. **Not archiving** — `inbox_count` flat while the pile sits there. Cheap per
   run, and it is what produced the backlog in the first place.

They pull in opposite directions. The rules are deliberately tuned so (1) is
rare and (2) is tolerated. Do not quietly retune that balance.

## Run the fixtures — before and after

`FIXTURES.md` is the eval set: real threads with settled verdicts. It is the only
thing standing between a plausible-sounding rule change and a regression.

Before you change anything, and again after, work each fixture from the current
`RULES.md` plus `CORRECTIONS.md` and write down the verdict those files actually
produce. Compare it to the recorded verdict.

- **Before:** a fixture that already fails is a bug in the rules as they stand.
  Fix that first. It is worth more than anything else you could do this week.
- **After:** a fixture that flipped was flipped by your change. Revert the
  change. A rule that cannot hold known-good answers is not an improvement,
  however good the reasoning behind it sounded.

Record both passes in `runs/review-YYYY-MM-DD.md`, one line per fixture. This is
the only point where the system checks itself against known-good answers instead
of against its own judgement. Do not skip it and do not summarise it — a pass you
did not actually work through is worse than no pass, because it launders a
regression as verified.

## The measurement — evidence, not opinion

Read `runs/*.md` for the last 7 days and `state.json`.

**The signal that matters:** for every thread the logs record as archived,
especially the close calls, check whether it is in the inbox now. If it is back,
Miles pulled it back — he overrode the call, and that is a wrong archive with a
name attached. Everything else here is inference. This is the only direct
evidence you get. Start here.

**The counter-signal:** `inbox_count` across the last 5 runs. Flat or rising
means the rules have gone too cautious and the question in `RULES.md` is being
asked wrong again.

## What you may change

- **Append to `CORRECTIONS.md`.** The main output. One dated line with its
  reason. A correction earns its place only if you can point at the run-log entry
  or the pulled-back thread that motivated it. No speculative rules.
- **Add a fixture to `FIXTURES.md`** when a judgement call got settled this week.
  Real threads with real verdicts only. An invented fixture is worse than none —
  it turns the eval set into fiction.
- **Edit `RULES.md`** only when the same correction has recurred three or more
  times and deserves promotion to a class rule, and only when the fixtures still
  pass after. Promoting one means deleting the correction lines it replaces, in
  the same commit.

## What you may not change

- **Never flip a verdict in `FIXTURES.md` to make a rule change pass.** If a
  change contradicts a fixture, the change is probably wrong. If the fixture is
  genuinely wrong, that is a separate commit that says why.
- **Never delete a `CORRECTIONS.md` line for looking stale.** It is append-only,
  and each line carries its reason precisely so a later run cannot talk itself
  into reverting it.
- **Never edit `state.json`.** That belongs to the triage.

## Finish

Commit as `review YYYY-MM-DD: <what changed>` and push.

If nothing earned a change, change nothing and say so in one line. A review that
edits nothing is a good week, not a failed run. The failure mode for this task is
inventing work to look useful.
