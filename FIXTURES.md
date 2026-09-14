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
| 22 | `express@airbnb.com` — Natasa/Milica/Ditte, host conversation after the stay ended and the last message is a pleasantry with no question in it | ARCHIVE | Complement to #2: #2 protects a person *waiting*, this is the same address once nobody is. Applied to three different hosts (09-10, 09-11, 09-14) with zero pullback; a reply on the same thread naturally puts it back in the inbox (09-11's Natasa is 09-10's Natasa after she sent a new message) — that is Gmail behaving normally, not Miles overriding the call |
| 23 | Forum Melbourne pre-sale, live window with a real deadline hours away | ARCHIVE | RULES' leave-examples (bill, form, collection) are all obligations he owes; a discretionary pre-sale is an opportunity, not one. Named individually in the brief with the deadline so it's still visible same-day. Recurred three times (Periphery 09-08, Paul Dempsey Karaoke 09-10, Soul Asylum 09-14), zero pullback — a judgment call, not a rule, since there's no fixed cutoff behind it |
| 24 | ENGIE bill, due date passed, no further message from ENGIE since (no failure notice, no new bill) | ARCHIVE | Flip side of #5: #5's More reminder stays because a live overdue/failed-payment notice is still active behind it. Here the date passed in silence — read as paid, now a record. Contrast with VicRoads (left in the inbox five runs straight 09-08→09-14): VicRoads' due date also passed, but with an active bank-reported payment failure behind it, so it stays. The signal is not "has the date passed" but "is there still live trouble behind it" |
| 25 | Anita (Mum) — two live threads same day, "My CV and website" (has an open question) and "Cv" (her CV attached, no question, her actual ask lives in the sibling thread) | split | Judge each thread on its own open question, never on a sibling thread's status. "Cv" archived, "My CV and website" stays. Held through 09-10, 09-11, 09-14 as further Anita threads came and went independently with no cross-contamination |
| 26 | The Orchard — overstock storage, "reply with label ID + UPCs by 11 Sep", deadline passed unmet | ARCHIVE | Kept the week before while the deadline was ahead (fixture-8 shape); once the reply-by date passed without a reply, it's dead as a request — archiving a missed deadline doesn't undo the miss, and the actual consequence (storage charges from Oct 2026) is a separate future event that will arrive as its own mail if it happens. First time this system reversed a call it had itself protected the week before, on nothing but the date moving |

## One case where the rules disagree with themselves

| 15 | `hello@account.dataforseo.com` — "API password", containing the credential |

Under the old rules this was protected as a stored credential. Under the current
rules the question is "would he miss it if it weren't in the inbox?" — and he
wouldn't; he'd search for it. **Current answer: ARCHIVE.**

That is a real change of behaviour caused by simplifying, not an oversight.
If it turns out to be wrong, it belongs in `CORRECTIONS.md` with a reason.
