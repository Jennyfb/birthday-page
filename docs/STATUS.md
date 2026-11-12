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
| 5   | Responsive + polish                     | Mobile-first thinking — most guests open this on a phone | ✅     |
| 6   | Link previews (Open Graph)              | Why a pasted link looks good or looks broken in a chat   | ✅     |
| 7   | Push to GitHub, enable Pages            | Deploying by pushing                                     | ✅     |
| 8   | Connect the custom domain               | DNS records, `CNAME`, HTTPS propagation                  | ✅     |

**🎉 Live at https://jennyfarstad.no** since 2026-11-12.

## Open questions

### ~~Which CSS framework?~~ — resolved: Pico.css (see D4)

### ~~Event details~~ — collected, see Event facts below

### ⚠️ Open: RSVP deadline vs. the moved date

The party moved from tirsdag 24. to **lørdag 28. november**, but the page still says
RSVP by **18. november** — which is onsdag, and only days away. The extra runway means
21.–22. november would still give Lille Ó plenty of notice.

Whatever the deadline, **the page has to be live and shared before it.** Steps 6–8
(link previews, deploy, domain) are now the critical path, not polish.

### Resolved: RSVP deadline needs a real date

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
| Date        | Lørdag 28. november 2026 (verified: 28.11.2026 is a Saturday)      |
| Time        | 19:30, chambre séparée until 22:00, then possibly drinks onward    |
| Venue       | Lille Ó — eget chambre séparée                                    |
| Address     | Sandakerveien 100a, 0484 Oslo                                     |
| Dress code  | Ingen krav. Lov å kle seg romantisk for anledningen                |
| Gifts       | Ingen gaver ønskes — middagen er gaven                            |
| RSVP by     | 21. november 2026                                                 |
| Domain      | jennyfarstad.no (apex, no `www`)                                  |
| RSVP how    | Melding på Messenger / Snap / SMS — hvilken kanal som helst        |
| Language    | Norsk (bokmål) → `lang="nb"`                                      |

## Leftovers

- [ ] `<meta name="robots" content="noindex, nofollow" />` not added. Without it the
      page — date, time and venue — is eligible for Google results under Jenny's name.
      Optional, but it is the only thing from the deploy checklist still open.
- [ ] `Jennyfb/Jennyfb.github.io` still has a `CNAME` file pointing at `ntnuoc.no`,
      a domain with no DNS records. Harmless now that this repo sets its own domain,
      but it is why project pages redirected somewhere unexpected. Clean up by
      deleting that file, or clearing the custom domain in that repo's Pages settings.
- [ ] Repo name is `birthay-page` (missing a `d`). Invisible to guests now that the
      custom domain works.

## Log

- **2026-10-31** — Project started. Decisions D1–D5 recorded. Scope fixed at one page.
- **2026-10-31** — Steps 0–1 done. Pico.css chosen (D4). Event facts collected;
  RSVP deadline set to 18. november. Assets renamed to `charlotte-27.jpg` / `.gif`.
- **2026-10-31** — Step 2: hero + `style.css` written. Theming done by reassigning
  Pico's `--pico-*` custom properties rather than overriding its selectors. Page
  pinned to `data-theme="light"` — the design is a paper card, dark mode is not
  meaningful for it. Banner uses the JPG; the 5.6 MB GIF is still in `assets/` as a
  possible swap (would need ffmpeg → MP4 first).
- **2026-11-06** — Pushed to GitHub (`Jennyfb/birthay-page`). Push initially failed
  with `RPC failed; HTTP 400`: the 5.6 MB GIF pushed the pack over git's default 1 MB
  `http.postBuffer`, forcing chunked transfer, which GitHub rejects. GIF removed from
  the repo; the JPG is the only asset now.
- **2026-11-12** — Date moved to lørdag 28. november, 19:30. Hero reworked to
  full-bleed: the photo is now a blurred CSS background fading into the page, with
  the Charlotte Lucas line typeset as a `<blockquote>` in a frosted-glass card. The
  blur is deliberate — the source is only 540×400, so upscaling it sharp would look
  mushy; blurring converts that into depth-of-field. `<h1>` restored to "Jenny blir
  27 år" so the page announces its actual subject.
- **2026-11-12** — **Deployed.** Live on https://jennyfarstad.no, Let's Encrypt
  certificate issued, HTTPS enforced. Four A records on the apex at Domeneshop,
  `www` CNAME redirecting to the apex. The initial `NotServedByPagesError` was the
  domain resolving to `parkedweb01.domeneshop.no` — the parking record had to be
  removed, not just added alongside. Verified: all assets 200, Open Graph tags
  complete including an absolute `og:image`.
