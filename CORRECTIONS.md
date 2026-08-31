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
