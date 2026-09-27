# Daily Sports Brief — Instructions

You are producing a personal daily sports newsletter for one reader and emailing it to them.
Follow this document exactly. Topic scope and priorities live in `topics.md`; the visual
layout lives in `template.html`. Past issues live in `archive/`.

## Delivery

- **To:** vishwanathovi@gmail.com
- **Subject:** `Daily Sports Brief — <Day, DD Mon YYYY>` (e.g. `Daily Sports Brief — Sun, 27 Sep 2026`)
- **Send with:** the Gmail connector (`send_message`, `htmlBody` = the rendered HTML, `body` = a short plain-text fallback).
- **Schedule:** every day at 9:00 AM IST (the Routine fires a few minutes early).

## Run steps

1. **Get the date.** Run `TZ=Asia/Kolkata date`. "Today" and every time in the email are IST.
   The coverage window is the **last 7 days** up to now.
2. **Read context.** Read `topics.md`, `template.html`, and the 3 most recent files in `archive/`.
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
4. **Pick the hero.** The single biggest story across all four sports in the window becomes the
   hero (one per issue). Priority tie-breaker: F1 race result > India men's cricket result >
   Grand Slam final > UFC title fight.
5. **Write the issue** using `template.html` components:
   - Hero → 1 headline, 1-sentence summary, 2–3 bullet highlights, source link.
   - One section per sport, in this order: Formula 1, UFC, Tennis, Cricket.
     - **Result card**: event name + date, the result (podium / winner + method / scoreline),
       then 2–3 bullets of key details. Link to the original report.
     - **News items**: 1–2 lines each, max 3 per sport, each with a source link.
     - **Upcoming event card**: event name, date, start time **IST** (convert from local/ET/UTC
       and double-check the day rolls over correctly), venue, and the main fights / key matchup.
   - If a sport has nothing in the window and nothing upcoming soon, show a single muted line:
     "Quiet week — nothing major." Do not pad.
   - Keep it tight: the whole email should be readable in ~3 minutes.
6. **Validate** before sending: every item has a working-looking source URL, all times say IST,
   no section exceeds its limits, HTML uses inline styles only (email clients strip `<style>`).
   Never use white or light text: many email clients strip or invert background colours, so
   all text must be dark and readable on a plain white background (keep the template's hero style).
7. **Send** the email (see Delivery).
8. **Archive.** Save a short markdown record to `archive/YYYY-MM-DD.md` (headlines + links,
   not the full HTML), commit it with message `newsletter: issue YYYY-MM-DD`, and push to the
   branch this folder lives on. If the push is refused, the email is still the deliverable —
   do not retry endlessly.

## Style

- Plain, factual, no hype. Numbers and names over adjectives.
- Bold the winner / key name in each result.
- Write times in 12-hour format with the day, e.g. `5:30 AM IST, Sun 4 Oct`.
