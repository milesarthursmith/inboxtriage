# Triage rules

`CORRECTIONS.md` beats everything here.

## The model

The inbox is an action queue. Gmail search is the filing system, so archiving is
free and reversible. Never apply labels. Read/unread carries no signal — Miles
opens mail on his phone without acting on it. Never scope a search to `is:unread`.

Archive with `unlabel_thread`, labelIds `["INBOX","UNREAD"]` — always both.

## Who is a person — derive it, never list it

A **conversation** is a thread where a real person other than Miles wrote a
message. Conversations are never archived by this task, at any age, unless
`CORRECTIONS.md` says otherwise or Miles says it is handled.

Do not maintain a list of people. Derive it:

- `in:sent` is everyone Miles has ever replied to. That is the correspondent set.
- For a sender you cannot place, search `from:<address> in:sent` — if he has
  written to them, it is a conversation.

A maintained list goes stale the moment someone new emails him. The Sent folder
never does.

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

- Any conversation (see above).
- Health **results, referrals, prescriptions**. Appointment *reminders and
  confirmations* expire once the appointment passes — logistics, not records.
- Travel documents for a trip that has not finished.
- Anything you have positive reason to believe is unpaid or owed.
- An open application or negotiation still running by email.
- Stored credentials the message says to keep.

## The run

1. **Noise** — `in:inbox category:promotions`, `in:inbox category:social`.
2. **Updates** — `in:inbox category:updates`, apply the expiry table. Main event.
3. **Recent** — `in:inbox newer_than:14d`. Only `get_thread` on possible
   conversations or replies.
4. **Backlog** — from `state.json` → `frontier`. Work `in:inbox before:<frontier>`,
   up to 80 threads. When a window returns only conversations, move the frontier
   forward and record it.

**`search_threads` has no sort parameter.** Gmail returns newest-first, always.
"Oldest first" against `older_than:Nd` is unimplementable and will silently
re-read the same recent slice forever. Absolute date windows only.

Do not `get_thread` anything you are about to archive. Judge from sender and
subject; use the derivation above when a sender is ambiguous.

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
