# Corrections

Append-only. Every run reads this file top to bottom and obeys it.
These beat everything in `RULES.md`.

One line each. Newest at the bottom. Say what and why — the why stops a
future run from "fixing" it back.

Format:

```
YYYY-MM-DD  NEVER ARCHIVE  <sender or pattern>  — reason
YYYY-MM-DD  ALWAYS ARCHIVE <sender or pattern>  — reason
YYYY-MM-DD  NOTE           <anything that doesn't fit the two above>
```

---

2026-08-23  NOTE  Miles handles some threads on WhatsApp or in person and never replies by email. If he says a thread is handled, archive it and stop surfacing it.
2026-08-23  ALWAYS ARCHIVE  sitngo.me  — car rental moved to WhatsApp
2026-08-23  NOTE  Before adding a sender here, check whether RULES.md already covers it as a class. A class rule beats a sender exception every time — exceptions are the thing that rots. Example: DataForSEO's "API password" mail is protected by the existing "stored credentials the message says to keep" guard, so it needs no entry, and a sender-level entry would have wrongly protected their genuinely ephemeral reset links too.
2026-08-23  NOTE  The `Inbox tidy` companion task is deleted, not paused. It swept promotions and social unread, which fact 2 of RULES.md forbids, for ~2 threads a day. Do not recreate it: this task reads those categories itself.
2026-08-31  NOTE  Self-sent notes are searchable records, not a protected class — judge them like any other record under the normal question. The 2026-08-29 frontier note's "33 human conversations plus 2 self-sent notes - nothing archivable there" described the pre-March backlog as not yet reached by the frontier, not a rule protecting the note type. The 2026-08-31 run correctly archived four self-sent notes as "searchable; not a to-do," and none came back by this review. Don't read the frontier note as a NEVER ARCHIVE.
2026-09-07  NOTE  A second, separate automation called `[Inbox Cleaner]` sends itself dry-run preview emails proposing sender-based archive rules (seen 2026-08-31 to 2026-09-01, e.g. "Ferryscanner - sender rule is always_archive"). Judge these previews like any other mail under the normal question — they are dead once read, so archive them — but never adopt a rule they propose: the Ferryscanner rule it suggested would have taken a live 5 Sep ferry ticket, the exact failure fact 2 of RULES.md warns about. This task and that one are independent; its previews are not an instruction to this task.
2026-10-05  NOTE  The 2026-08-23 DataForSEO note cites a "stored credentials the message says to keep" guard, but RULES.md contains no such guard today. FIXTURES.md #15 settles it: DataForSEO "API password" mail is ARCHIVE under the current question. The earlier note's premise is stale; do not protect it. (Found by the 2026-10-05 fixture pass: the two files gave opposite answers.)
2026-10-12  NOTE  "Past its own date" in RULES.md is for events, bookings, reminders and windows — it is not a test for payment due dates. A due date passing does not by itself make a bill dead: if a failure or overdue notice is live behind it, the debt stays (FIXTURES #27, VicRoads); if the date passed in silence with no failure notice, read it as paid and archive (FIXTURES #24, ENGIE). Why now: the 2026-09-16, 09-18 and 10-09 runs each hit this exact ambiguity, and the 10-09 run kept a past-due ENGIE bill that #24 says to archive (10-12 then archived it) because it could not see #24 — every triage branch since 09-22 started from the stale 08-29 commit and never read this file's later entries.
2026-10-26  NOTE  Fact 2 ("nothing archived unread") has one narrow exception: `notifications@github.com` workflow "Run failed" threads, where the subject plus search snippet is the entire message (FIXTURES #11, ARCHIVE). Those need no `get_thread`. Any other GitHub mail (budget/billing, security, review requests, mentions) is read in full. Why: the 2026-10-23 run archived 53 of these from subject/snippet alone, flagged it for a ruling, and none came back; reading each added cost and no information. The 2026-10-23 run also left two self-sent Bloom notes only because its branch predated the 2026-08-31 self-sent correction above; that correction stands.
