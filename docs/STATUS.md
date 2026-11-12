# Status & roadmap

Updated: 2026-10-31

## Where we are

**Step 1 — HTML skeleton.** Step 0 done: repo initialised, structure in place,
`index.html` and `style.css` created (empty). CSS framework decided: Pico.css.

## The plan

| #   | Step                                    | What you learn                                           | State  |
| --- | --------------------------------------- | -------------------------------------------------------- | ------ |
| 0   | Repo + folder structure, git init       | Why a project has a shape before it has code             | ✅     |
| 1   | HTML skeleton, semantic structure       | Documents vs. divs; the `<head>` nobody reads            | ✅     |
| 2   | The banner / hero                       | Layout, type scale, making one element carry the mood    | 🔨 now |
| 3   | Details section (when, where, map link) | Structured content; `<time>`; linking to maps            | ⬜     |
| 4   | RSVP section                            | `sms:` / `wa.me` / `mailto:` links and their gotchas     | ⬜     |
| 5   | Responsive + polish                     | Mobile-first thinking — most guests open this on a phone | ⬜     |
| 6   | Link previews (Open Graph)              | Why a pasted link looks good or looks broken in a chat   | ⬜     |
| 7   | Push to GitHub, enable Pages            | Deploying by pushing                                     | ⬜     |
| 8   | Connect the custom domain               | DNS records, `CNAME`, HTTPS propagation                  | ⬜     |

## Open questions

### ~~Which CSS framework?~~ — resolved: Pico.css (see D4)

### ~~Event details~~ — collected, see Event facts below

### Open: RSVP deadline needs a real date

"Om en uke" was relative to the day it was written. A reader can't resolve that —
put an actual date on the page. Counting a week from 2026-10-31 gives **lørdag 7.
november**, but pick whatever is genuinely useful for booking the table.

### Open: does Lille Ó need a headcount by a certain date?

If the restaurant needs final numbers by date X, the RSVP deadline should be X minus
a couple of days, not an arbitrary week.

---

## Event facts

The single source of truth for page copy. If it's not here, it doesn't go on the page.

| Field       | Value                                                             |
| ----------- | ----------------------------------------------------------------- |
| Occasion    | Jenny blir 27 år                                                  |
| Theme       | _Pride & Prejudice_ — the Charlotte Lucas "I'm 27 years old" scene |
| Date        | Tirsdag 24. november 2026 (verified: 24.11.2026 is a Tuesday)      |
| Time        | 18:30                                                             |
| Venue       | Lille Ó — eget chambre séparée                                    |
| Address     | Sandakerveien 100a, 0484 Oslo                                     |
| Dress code  | Ingen krav. Lov å kle seg romantisk for anledningen                |
| Gifts       | Ingen gaver ønskes — middagen er gaven                            |
| RSVP by     | 18.november                                 |
| RSVP how    | Melding på Messenger / Snap / SMS — hvilken kanal som helst        |
| Language    | Norsk (bokmål) → `lang="nb"`                                      |

## Log

- **2026-10-31** — Project started. Decisions D1–D5 recorded. Scope fixed at one page.
- **2026-10-31** — Steps 0–1 done. Pico.css chosen (D4). Event facts collected;
  RSVP deadline set to 18. november. Assets renamed to `charlotte-27.jpg` / `.gif`.
- **2026-10-31** — Step 2: hero + `style.css` written. Theming done by reassigning
  Pico's `--pico-*` custom properties rather than overriding its selectors. Page
  pinned to `data-theme="light"` — the design is a paper card, dark mode is not
  meaningful for it. Banner uses the JPG; the 5.6 MB GIF is still in `assets/` as a
  possible swap (would need ffmpeg → MP4 first).
