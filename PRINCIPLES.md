# Principles

Facts about Gmail, not preferences. These do not change.

**Every rule in `RULES.md` must trace to one of these. If a rule cannot be
traced to a principle, delete the rule — it is a guess wearing a uniform.**

---

**1. Archiving is not deleting.** `unlabel_thread` removes the INBOX label.
The thread stays in All Mail permanently and is one search away.

*Therefore:* a wrong archive costs attention, never data. Guard only things
that need action inside a window. When torn, archive.

**2. The one exception.** Removing `UNREAD` marks a thread read, and that flag
does not come back.

*Therefore:* the brief must list what was archived. That list is the only
recovery index.

**3. Search is how mail is retrieved. Inbox and labels are views, not storage.**

*Therefore:* records, receipts, credentials, results and past bookings do not
need to sit in the inbox. Nobody scrolls for those — they search.

**4. `search_threads` has no sort parameter. Gmail returns newest-first, always.**

*Therefore:* "work oldest first" against `older_than:Nd` is unimplementable and
will silently re-read the same recent slice forever. Absolute date windows only.

**5. Queries match at thread level — a thread matches if any message in it does.**

*Therefore:* `-from:X` safely excludes the whole thread. But `category:updates`
can match a thread containing a human reply, so category alone never proves a
thread is automated.

**6. Gmail already classifies mail.** `category:promotions`, `social`,
`updates`, `personal` are a free, maintained classifier.

*Therefore:* use them before writing keyword heuristics. `category:updates` is
the highest-yield archivable bucket.

**7. `in:sent` proves someone IS a correspondent. It does not prove someone
ISN'T.** It is a one-way test. Everyone Miles has replied to is there; everyone
who has just written to him for the first time is not.

*Therefore:* use it to confirm, never to exclude. A first email from a new
client, recruiter or solicitor has no history by definition — and first contact
is often the most valuable mail in the inbox. For an unknown sender the question
is whether a person wrote the message, not whether there is history.

*Therefore also:* no list of people, and no derivation, can settle this from a
sender address alone. See principle 9.

**9. Deciding whether a person wrote something requires reading it.** No
address pattern, Gmail category or search operator settles it. `rent@sitngo.me`
is a person; `hello@exa.ai` is not; neither is knowable from the address.

*Therefore:* the cost of triage is reading, and it cannot be optimised away.
What CAN be skipped is reading the obviously-automated bulk — `category:promotions`
and `category:social`, no-reply and notification-only sending domains. Anything
outside that gets read before it gets archived. A rule that archives unread mail
on category alone is unsafe, however convenient.

**8. There is no batch label API.** One call per thread to archive.

*Therefore:* the expensive part is classification, not archiving. Let Gmail do
the set arithmetic with one query rather than reading threads one at a time.

---

## The question to ask

Not *"could this be important?"* — almost anything could.

Ask *"would he miss it if it were not in the inbox?"*

Principle 1 makes the first question meaningless and the second one the only
one that matters. Asking the wrong one is what produced a 200-thread backlog
of month-old dead reminders.
