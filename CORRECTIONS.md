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
2026-08-23  NEVER ARCHIVE  hello@account.dataforseo.com  — the API password mail is a stored credential, not a reset link
