# Daily Sports Brief — Instructions

You are producing a personal daily sports newsletter for one reader and emailing it to them.
Follow this document exactly. Topic scope and priorities live in `topics.md`; the visual
layout lives in `template.html`. Past issues are the emails already sent (see step 2).

## Delivery

- **To:** vishwanathovi@gmail.com
- **Subject:** `Daily Sports Brief — <Day, DD Mon YYYY>` (e.g. `Daily Sports Brief — Sun, 27 Sep 2026`)
- **Send with:** the Gmail connector (`send_message`, `htmlBody` = the rendered HTML, `body` = a short plain-text fallback).
  `htmlBody` must start directly with the outer `<table ...>`. Do **not** include `<!doctype>`,
  `<html>`, `<head>`, `<body>` tags or HTML comments: Gmail shows them as literal text at the
  top of the email.
- **Schedule:** every day at 9:00 AM IST (the Routine fires a few minutes early).

## Run steps

1. **Get the date.** Run `TZ=Asia/Kolkata date`. "Today" and every time in the email are IST.
   The coverage window is the **last 7 days** up to now.
2. **Read context.** Read `topics.md` and `template.html`. Then find the recent issues in Gmail:
   `search_threads` with `subject:"Daily Sports Brief" in:sent newer_than:4d`, and read the
   latest 2–3 with `get_message` (`messageFormat: PLAIN_TEXT`). Ignore subjects starting with
   `[TEST]`. If a past issue says a result was pending ("in progress", "full result tomorrow"),
   report the final result today.
   Anything already covered in a recent issue should not be repeated as a full story unless
   there is a genuinely new development (then say what changed).
3. **Research each sport** (see `topics.md` for scope) with web search. For each sport find:
   - **Results** — events that finished in the last 7 days (race, card, Slam, match/series).
   - **Top news** — only prominent items: contracts/transfers, injuries ruling someone out,
     title changes, suspensions, major announcements. Skip rumours, previews and opinion pieces.
   - **Upcoming** — the next relevant event (within ~14 days), with date and start time in IST.
   Cross-check key facts (winner, score, date) against at least two results. If page fetches
   are blocked by the network, rely on search-result snippets from reputable outlets and link those.
   Never invent a result, score, time or quote. If something is unconfirmed, leave it out.
4. **Pick the top story.** The single biggest story across all four sports in the window
   opens the issue (one per issue). Priority tie-breaker: F1 race result > India men's cricket
   result > Grand Slam final > UFC title fight.
5. **Write the issue** with the blocks in `template.html` (Bloomberg India Edition style:
   one plain column, black rules between sections, links inside sentences, no cards or emoji):
   - **Masthead + intro**: keep the fixed italic welcome line; write a one-sentence
     "Today: …" teaser naming the 2–3 biggest items.
   - **Top story section**: a short headline-style title (e.g. "Russell Holds On in Baku"),
     one paragraph (2–3 sentences), then "Key moments" with 2–3 bullets.
   - **One section per sport**, in this order: Formula 1, UFC, Tennis, Cricket. Don't repeat
     the top story in its sport's section.
     - **Results**: a bold subhead ("Rosas Jr. stops Barcelos in Vegas"), then 1–2 short
       paragraphs: result (podium / winner + method + round / scoreline) and key details.
     - **News**: 1–2 sentences each, max 3 per sport, with the source link inside the sentence.
     - If a sport has nothing in the window, use the grey quiet-week line. Do not pad.
   - **Coming Up**: every upcoming event from all sports in one list, sorted by date (next
     ~14 days, plus the next Grand Slam if it's within 30 days). Each row has the event name
     (linked), day, date, start time **in IST** (convert from local/ET/UTC and check the day
     rolls over correctly) and venue. UFC rows list the main card. The right-hand
     **days-left** cell is calendar days from the issue date to the event date, both in IST:
     0 → "Today" / "live", 1 → "1" / "day left", n → "n" / "days left". Compute it with
     `date`, don't estimate it.
   - Keep it tight: the whole email should be readable in ~3 minutes.
6. **Validate** before sending: every item has a source link, all times say IST, days-left
   numbers match the dates, no section exceeds its limits, and the HTML uses inline styles
   only (email clients strip `<style>`). Never use white or light text: many email clients
   strip or invert background colours, so all text must be readable on plain white.
7. **Send** the email (see Delivery).
8. **Done.** The sent email is the record; don't commit or push anything to the repo.
   Finish by replying with the subject, the Gmail message id and one line per section.

## Style

- Plain, factual, no hype. Numbers and names over adjectives.
- Bold the winner / key name in each result.
- Write times in 12-hour format with the day, e.g. `5:30 AM IST, Sun 4 Oct`.
