# inbox

Memory for the weekday inbox triage task (`Inbox brief (7am)`).

The scheduled task holds no state between runs — every firing is a fresh session.
This repo is where it remembers.

| File | Who writes it | What it holds |
|---|---|---|
| `RULES.md` | Claude, on request | The triage logic. Change this to change behaviour. |
| `CORRECTIONS.md` | Miles | Overrides. Append-only. Every run reads it and obeys. |
| `state.json` | Each run | Backlog frontier, inbox counts, last 5 runs. |

## How a run works

```
git pull
read RULES.md, CORRECTIONS.md, state.json
triage the inbox
write state.json
git commit -am "triage YYYY-MM-DD: archived N, inbox M"
git push
```

`git log` is the audit trail. Every archive decision is in a commit.

## If something was archived wrongly

Add a line to `CORRECTIONS.md` and push. The next run reads it and it sticks.
Nothing is ever deleted — archived mail is in All Mail, so search the sender
and re-apply Inbox to get it back.
