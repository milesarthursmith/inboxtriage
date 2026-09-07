# Fixtures

Real threads with known verdicts. Run the rules against these before changing
them — if a change flips one of these answers, either the change is wrong or
this file needs updating with a reason. Never both silently.

| # | Thread | Verdict | Why |
|---|---|---|---|
| 1 | Latitude one-time code for a Ferryscanner purchase, 23 Aug | ARCHIVE | Code used, purchase completed |
| 2 | `express@airbnb.com` — Ditte asking arrival time, 22 Jul | **LEAVE** | A person is waiting. No-reply address, human message — the case that killed sender-based rules |
| 3 | Pharmacy reorder reminder, filed by Gmail under Promotions | **LEAVE** | Live reorder. Proves `category:promotions` is not a verdict |
| 4 | ENGIE bill 22 Jun, with July and August bills behind it | ARCHIVE | Superseded |
| 5 | More — "friendly reminder to pay your overdue account", 24 Jul | **LEAVE** | Genuinely unpaid |
| 6 | `rent@sitngo.me` car rental offer | ARCHIVE | CORRECTIONS says so — moved to WhatsApp. Tests that CORRECTIONS beats RULES |
| 7 | Calendar reminder, MIFF 22 Aug, read on 23 Aug | ARCHIVE | Past its own date |
| 8 | Anaconda "ready for collection", before Miles said he'd collected it | **LEAVE** | Open action |
| 9 | Same thread, after Miles said "anaconda picked up" | ARCHIVE | He said it's handled |
| 10 | `messaging-digest-noreply@linkedin.com` — "Dan just messaged you" | ARCHIVE | The message lives in LinkedIn. But name the senders in the brief |
| 11 | GitHub Actions "Run failed" | ARCHIVE | Dead on arrival |
| 12 | Etihad booking 8SG35V, trip 24 Aug, read 23 Aug | **LEAVE** | Deadline ahead |
| 13 | Same booking, read in October | ARCHIVE | Trip finished |
| 14 | First email from a person with no reply history | **LEAVE** | Cannot be ruled out from the address. First contact is often the most valuable mail |
| 16 | Gabriella "Evals" course-login thread, 5 Jun, 2 unread messages, never replied | ARCHIVE | Real person, but no question and no deadline — she never asked him anything. ~3 months stale, personal threads like this get handled offline per CORRECTIONS 2026-08-23. Settled 2026-08-29, checked against the inbox again on 2026-08-31 review: no pullback |
| 17 | Gabriella-forwarded Flightnetwork booking CPH->LHR 13 Sep, "Sent from my iPhone" wrapper | ARCHIVE | Opened the HTML and checked the passenger list — it names only her, booking 1148-204-454. His own CPH->LHR is a separate ticket (SAS X8GTMV) that stays. Checked 2026-09-01, no pullback by 2026-09-07 |
| 18 | Same sender, same day, forwarded Gotogate booking FCO->TIV, "Sent from my iPhone" wrapper | **LEAVE** | Same shape as #17, opposite verdict — the passenger list names MILES ARTHUR SMITH. This is the only copy of his own itinerary he holds. Pairs with #17 to show the sender/wrapper decides nothing; only opening the booking and reading the passenger names does |
| 19 | Fairfield CMC referral to a psychologist, unread ~3 weeks | **LEAVE** | Live referral, still within a window where booking is plausible |
| 20 | Fairfield CMC referral to pathology, same sender/shape, unread ~3 months | ARCHIVE | Sat unactioned long enough to read as abandoned rather than pending. Recency is the only thing distinguishing this from #19 — flagged as the weakest call in the run that made it, held through the following week with no pullback |
| 21 | Dan Fleming, live job-process thread — he proposed holding a case study, Miles agreed and named a date, nothing outstanding on Miles's side | ARCHIVE | Mirror of #14: a real person and an open process, but the ball is in their court, not his. Their next message re-surfaces the thread; archiving it now costs nothing |

## One case where the rules disagree with themselves

| 15 | `hello@account.dataforseo.com` — "API password", containing the credential |

Under the old rules this was protected as a stored credential. Under the current
rules the question is "would he miss it if it weren't in the inbox?" — and he
wouldn't; he'd search for it. **Current answer: ARCHIVE.**

That is a real change of behaviour caused by simplifying, not an oversight.
If it turns out to be wrong, it belongs in `CORRECTIONS.md` with a reason.
