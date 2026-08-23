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

**7. `in:sent` is ground truth for who Miles corresponds with.**

*Therefore:* never maintain a list of people. Derive it. A list goes stale the
moment someone new writes; the Sent folder never does.

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
