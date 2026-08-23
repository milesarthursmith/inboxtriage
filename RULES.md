# Inbox triage

Memory for the weekday 7am task. Every run is a fresh session — this is what it
reads. `CORRECTIONS.md` beats this file.

## Four facts about Gmail

1. **Archiving is not deleting.** Everything stays in All Mail, one search away.
   A wrong archive costs attention, not data. When torn, archive.
2. **Nothing is safe to archive unread.** Not by sender, not by Gmail category.
   `express@airbnb.com` is a no-reply address that relays real people; Gmail
   files pharmacy reminders and live flight bookings under Promotions. Read it,
   or leave it. *One accepted exception:* the companion `Inbox tidy` task sweeps
   `category:promotions` and `category:social` unread every two hours. That is a
   deliberate risk, taken because it works — promotions sits at ~2 threads — and
   it is also why a pharmacy reminder once ended up in the sweep. This task does
   not re-sweep those categories. It reads what tidy left.
3. **`search_threads` has no sort parameter** — always newest-first. "Oldest
   first" is unimplementable. Use absolute date windows.
4. **Removing `UNREAD` can't be undone**, so the brief must list what was
   archived. That list is the only recovery index.

## The job

Read the inbox newest-first, up to 80 threads, then the backlog window in
`state.json`. For each thread ask one question:

> **Would he miss it if it weren't in the inbox?**

Not "could this be important" — almost anything could. Asking the wrong question
is what produced a 200-thread backlog of month-old dead reminders.

**Leave it** if a real person is waiting on a reply, or there's an action with a
deadline still ahead — an unpaid bill, a form, an order to collect.

**Archive everything else.** Dead codes, past bookings, delivered parcels,
superseded bills, confirmations, receipts, records. All retrievable by search,
none missed.

Two checks the question won't prompt on its own — do them explicitly:

- **Superseded?** For a bill, statement or declined payment, look for a later
  message from the same sender. If one exists, this is a record.
- **Past its own date?** "Renews on 21 July", an appointment, a booking, a
  delivery window — compare it to today, not to how recently it arrived.

Archive with `unlabel_thread`, labelIds `["INBOX","UNREAD"]`. Never apply
labels. Read/unread carries no signal — he opens mail on his phone without
acting on it.

## The brief

One self-contained HTML file, inline CSS, phone-first, via `SendUserFile`:

1. **Waiting on you** — sender, one line, a complete draft reply. Never create
   Gmail drafts, never send.
2. **Open actions** — deadlines, unpaid bills, applications.
3. **Archived** — this is the review, and it happens after the fact, so make it
   readable. Counts by sender for the bulk. But list **individually, with a
   one-line reason**, anything that was a close call: mail from a real person's
   address, anything with money or a date in it, anything you hesitated over.
   Fifty Uber receipts are one line. One judgement call is one line each.

Then update `state.json` — `frontier`, `inbox_count`, last 5 runs — and push.
**If `inbox_count` hasn't fallen across 5 runs, say so at the top of the brief.**
That alarm is the thing that was missing while this ran for two weeks without
clearing anything.

Push a notification only if something genuinely needs him today.
