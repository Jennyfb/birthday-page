# Status & roadmap

Updated: 2026-10-31

## Where we are

**Step 0 — project setup.** In progress.

## The plan

| #   | Step                                    | What you learn                                           | State  |
| --- | --------------------------------------- | -------------------------------------------------------- | ------ |
| 0   | Repo + folder structure, git init       | Why a project has a shape before it has code             | 🔨 now |
| 1   | HTML skeleton, semantic structure       | Documents vs. divs; the `<head>` nobody reads            | ⬜     |
| 2   | The banner / hero                       | Layout, type scale, making one element carry the mood    | ⬜     |
| 3   | Details section (when, where, map link) | Structured content; `<time>`; linking to maps            | ⬜     |
| 4   | RSVP section                            | `sms:` / `wa.me` / `mailto:` links and their gotchas     | ⬜     |
| 5   | Responsive + polish                     | Mobile-first thinking — most guests open this on a phone | ⬜     |
| 6   | Link previews (Open Graph)              | Why a pasted link looks good or looks broken in a chat   | ⬜     |
| 7   | Push to GitHub, enable Pages            | Deploying by pushing                                     | ⬜     |
| 8   | Connect the custom domain               | DNS records, `CNAME`, HTTPS propagation                  | ⬜     |

## Open questions

### Which CSS framework? (blocks step 1)

Two genuinely different answers:

- **Pico.css** — _classless_. You write `<h1>`, `<article>`, `<button>` and it looks
  good with no classes at all. ~80KB, one `<link>` tag, no JavaScript. Fits a
  content page like this almost exactly.
- **Tailwind via `cdn.tailwindcss.com`** — a ~400KB _JavaScript_ file that scans your
  markup in the browser and generates CSS at runtime. Tailwind's own docs say not to
  use it in production. It causes a visible flash of unstyled content on slow phone
  connections — which is every guest opening this link on mobile data.

Recommendation: **Pico.css**, with our own `style.css` for the banner and anything
that should feel personal. Switching later is a one-line change.

### Event details needed (blocks step 2–3)

- [ ] Which birthday / what the occasion is called
- [ ] Date and start time (and rough end time?)
- [ ] Venue name + full address
- [ ] Anything guests should know: dress code, food, gifts, parking/transit
- [ ] RSVP deadline
- [ ] Which contact channel(s) for RSVP, and the number/handle to use
- [ ] Language — Norwegian or English?

## Log

- **2026-10-31** — Project started. Decisions D1–D5 recorded. Scope fixed at one page.
