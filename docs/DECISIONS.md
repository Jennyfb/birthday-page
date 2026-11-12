# Technical decisions

Short records of _what_ we chose and _why_. If a choice gets reversed later, don't
delete the entry — add a note at the bottom of it. The reasoning is worth more than
the conclusion.

---

## D1 — Static site, no backend

**Decision:** The site is plain files served as-is. No server, no database, no runtime.

**Why:** It's a one-page invitation for a single evening. A backend would be
something to secure, pay for, and remember to shut down. Static files are free,
fast, and can't crash.

**Cost:** Anything that needs to _store_ data (like collecting RSVPs) has to happen
somewhere else. See D2.

---

## D2 — RSVP by contact link, not a form

**Decision:** The page tells people to reach the host directly and gives tappable
links (`sms:`, WhatsApp `wa.me`, `mailto:`). Nothing is submitted to the page.

**Why:** Keeps D1 intact with zero dependencies. No third-party service, no free-tier
quota, no spam filtering, no privacy question about where friends' names are stored.
For a guest list of friends, the host's phone is already the database.

**Cost:** No automatic guest list. The host tallies replies manually. Acceptable at
this scale — revisit only if the invite list gets large.

---

## D3 — Hosting on GitHub Pages

**Decision:** Repo on GitHub, served via GitHub Pages, deployed by pushing to the
default branch.

**Why:** The source and the deploy target are the same place, so there's one thing to
learn instead of two. Free, supports custom domains with automatic HTTPS.

**Cost:** Static only. If the RSVP approach ever changes to something needing a
server-side function, we'd move to Cloudflare Pages or Netlify. That migration is
cheap — it's the same files.

---

## D4 — CSS framework from CDN

**Decision:** Hand-written semantic HTML, with base styling pulled from a CSS
framework over a CDN, plus a small local stylesheet for the parts that should look
custom.

**Why:** Avoids a build step (keeps D1 honest) while skipping the tedious part of CSS
— resets, typography scale, sensible form and button defaults.

**Resolved 2026-10-31: Pico.css**, loaded from jsDelivr, with our own `style.css`
layered on top.

Pico is _classless_ — it styles semantic elements directly, so `<h1>`, `<article>`
and `<button>` look good with no class attributes at all. That matches the goal
("look nice without CSS wizardry") and keeps the HTML readable.

Tailwind was rejected for this project: its CDN build is a ~400KB JavaScript file
that generates CSS in the browser at runtime, causing a flash of unstyled content on
mobile connections. Using Tailwind properly requires a build step, which contradicts
D1. Tailwind remains the better choice on projects that already have a build
pipeline — it loses here on context, not on merit.

**Cost:** Pico has opinions. Anything that should look distinctly non-default — the
banner especially — we write ourselves in `style.css`. That's intentional: the parts
that carry personality are the parts worth hand-writing.

---

## D5 — No JavaScript build step, minimal JS

**Decision:** Any JavaScript is a handful of lines in a plain `.js` file or inline.

**Why:** A birthday invite that needs a bundler has lost the plot. The page must work
if JS fails — all critical information (when, where, how to reply) lives in the HTML.

---

## D6 — Custom domain `jennyfarstad.no`

**Decision:** The invitation is served from the apex domain `jennyfarstad.no`,
pointed at GitHub Pages. The domain is configured before the link is shared.

**Why:** Connecting the domain after sharing means chat apps have already cached
preview cards against the `github.io` URL, and those caches are not under our
control. Open Graph tags also need absolute URLs, so the final hostname has to be
decided before they can be written.

**Cost:** DNS propagation plus certificate issuance before the link is usable.
Started 2026-11-12 with the party on 2026-11-28, so there is ample slack.

---

## Deliberately not doing

- **Analytics.** Not worth the cookie banner for an invite.
- **A countdown timer.** Tempting, but it's the first thing to break and adds a JS
  dependency for decoration. Reconsider at the polish stage if there's appetite.
- **Multiple pages.** One page. If it needs navigation, it's too big.
