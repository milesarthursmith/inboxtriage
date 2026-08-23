# Triage rules

Read `PRINCIPLES.md` first. Every rule below derives from a principle there.
If you find one that doesn't, it is a guess — delete it rather than obey it.

`CORRECTIONS.md` beats everything here.

## The model

The inbox is an action queue. Gmail search is the filing system, so archiving is
free and reversible. Never apply labels. Read/unread carries no signal — Miles
opens mail on his phone without acting on it. Never scope a search to `is:unread`.

Archive with `unlabel_thread`, labelIds `["INBOX","UNREAD"]` — always both.

## Who is a person — read, don't guess

A **conversation** is a thread where a real person other than Miles wrote a
message. Conversations are never archived by this task, at any age, unless
`CORRECTIONS.md` says otherwise or Miles says it is handled.

Do not maintain a list of people, and do not try to derive one either.
Per principle 7, `from:<address> in:sent` confirms a correspondent but can
never rule one out — a first-time sender has no history, and that is often the
mail that matters most.

Per principle 8, this cannot be settled from an address. So:

- `category:promotions` and `category:social` → archive unread. Safe.
- No-reply and notification-only sending domains → archive unread. Safe.
- **Everything else gets read before it gets archived.** That is the cost of
  the job. It cannot be optimised away, and a run that archives on category
  alone is unsafe however fast it is.

Marketing with a human signature, sales sequences, no-reply addresses and
notification bots are NOT conversations. Mail Miles sent to himself is NOT a
conversation.

Mark each conversation **waiting on you** (they wrote last) or **waiting on
them** (Miles wrote last).

## Expiry by class

Automated mail carries its own expiry. Use it. Age alone is not a rule — a
month-old dead reminder is dead, a two-day-old unpaid bill is not.

| Class | Dead when |
|---|---|
| One-time codes, OTP | On use, or 5–10 min |
| Magic / sign-in links | On use, or 5–15 min |
| Password & API-password resets | On use, or 15–60 min — single-use |
| Email / age / identity verification | On success, or 24 h |
| Calendar & appointment reminders | The event has passed |
| Bookings (venue, table, travel) | End of the booking |
| Delivery & shipping tracking | On delivery |
| Order confirmations | Delivered or collected |
| CI / build / deploy notifications | On arrival |
| "Renews on X" / "expires on X" | After X |
| Bills & statements | A later statement from the same sender arrives |
| Payment-declined notices | A later successful payment appears |
| Sign-in / new-device alerts | 48 h, if no action was taken |
| Welcome / onboarding / product marketing | On arrival |

Window still open **and** Miles still has to do something → **open action**.
Leave it and list it.

`category:updates` is Gmail's own "no action needed" classification and is the
highest-yield archivable bucket here.

## Hard guards — never archive

Archiving is not deleting. Everything archived stays in All Mail and is one
search away. So a wrong archive does not lose data — it loses **attention**.
That is the only harm, and it is the only thing worth guarding against.

Which means a guard earns its place only if the thing needs action inside a
window. Two do:

- **A conversation where someone is waiting on Miles.**
- **An open action with a deadline ahead** — an unpaid bill, a form, an
  application, an order to collect.

That is the whole list.

Records, credentials, health results, past travel documents, receipts and
statements are retrieved by *searching* for them, never by scrolling the inbox.
Archiving those costs nothing. Do not build guards for them.

When genuinely torn: archive. It is reversible, the brief lists what went, and
an inbox nobody trusts to be current is worse than one missing a receipt.

## The run

1. **Noise** — `in:inbox category:promotions`, `in:inbox category:social`.
   Archive unread. This is the only unread-safe bucket.
2. **Updates** — `in:inbox category:updates`. Sort into two piles by sender:
   structurally automated (no-reply, notification-only domains) → archive per
   the expiry table; everything else → read it first. Per principle 5 the
   category label does not prove a thread is automated, so it cannot license
   an unread archive on its own.
3. **Recent** — `in:inbox newer_than:14d`. Read anything that could be a person.
4. **Backlog** — from `state.json` → `frontier`. Work `in:inbox before:<frontier>`,
   same two-pile split. When a window returns only conversations, move the
   frontier forward and record it.

**`search_threads` has no sort parameter.** Gmail returns newest-first, always.
"Oldest first" against `older_than:Nd` is unimplementable and will silently
re-read the same recent slice forever. Absolute date windows only.

Reading is the cost of the job. Budget for it rather than designing around it.
A run that gets through less mail but reads what it archives is doing better
work than one that clears the backlog blind.

## Writing state

Every run updates `state.json`: `frontier`, `inbox_count`, append to `runs`
(keep the last 5). Then commit and push.

**If `inbox_count` has not fallen across the last 5 runs, say so at the top of
the brief.** That is the alarm that was missing when this ran for two weeks
without clearing anything.

## The brief

One self-contained HTML file, inline CSS, no external requests, single column,
phone-first. Deliver with `SendUserFile`.

1. **Waiting on you** — sender, one-line summary, a complete draft reply in a
   distinct block. Longest-waiting first, with days. Use `[...]` for facts not
   in the thread. Never create Gmail drafts. Never send.
2. **Waiting on them** — open loops, days waiting.
3. **Open actions** — live deadlines, unpaid bills, applications.
4. **Archived** — count by sender, so any can be undone.

Header: measured totals after the run, and the inbox trend from `state.json`.
Never report the slice you processed as the whole inbox.

Push a notification only if something genuinely needs Miles today.
