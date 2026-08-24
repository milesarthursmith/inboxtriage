# Weekly review

Memory for the Sunday review task. It reads a week of runs and edits the rules.
It does not triage. It does not touch the inbox except to read it.

## The two failure modes

1. **Wrong archive** — something he wanted was taken out of the inbox. Expensive:
   he has to notice it is missing before he can go looking.
2. **Not archiving** — `inbox_count` flat while the backlog sits there. Cheap per
   run, but it is what produced a 200-thread backlog once already.

They pull in opposite directions. RULES.md is deliberately tuned toward (1)
being rare and (2) being tolerated. Do not quietly retune that.

## The measurement — evidence, not opinion

Read `runs/*.md` for the last 7 days and `state.json`.

**The signal that matters:** for every thread the logs record as archived,
especially the close calls, check whether it is in the inbox now. Search
`in:inbox` for it. If it is back, Miles pulled it back — he overrode the call,
and that is a wrong archive with a name attached. Everything else here is
inference. This is the only direct evidence you get, so start here.

**The counter-signal:** `inbox_count` across the last 5 runs. Flat or rising
means the rules have gone too cautious and the question in RULES.md is being
asked wrong again.

## What you may change

- **Append to `CORRECTIONS.md`.** This is the main output. One dated line with
  the reason. A correction earns its place only if you can point at the run-log
  entry or the pulled-back thread that motivated it. No speculative rules.
- **Add a fixture to `FIXTURES.md`** when a judgement call got settled this week.
  Real threads with real verdicts only. An invented fixture is worse than none.
- **Edit `RULES.md`** only when the same correction has come up three or more
  times and deserves promotion to a class rule. `CORRECTIONS.md` is where
  exceptions go to be tested; `RULES.md` is where the survivors end up. When you
  promote one, delete the correction lines it replaces, in the same commit.

## What you may not change

- **Never flip a verdict in `FIXTURES.md` to make a rule change pass.** If a
  change contradicts a fixture, the change is probably wrong. If the fixture is
  genuinely wrong, that is a separate commit that says why.
- **Never delete a `CORRECTIONS.md` line for looking stale.** It is append-only
  and each line carries its reason precisely so a later run cannot talk itself
  into reverting it.
- **Never edit `state.json`.** That belongs to the triage.

## Finish

Commit as `review YYYY-MM-DD: <what changed>` and push.

If nothing earned a change, change nothing and say so in one line. A review that
edits nothing is a good week, not a failed run. The failure mode for this task is
inventing work to look useful.
