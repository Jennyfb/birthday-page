# Deploying to GitHub Pages on jennyfarstad.no

Work through this top to bottom. Steps 1–3 are quick; step 4 is mostly waiting.

---

## 1. Open Graph tags

Add to `<head>` in `index.html`, after the `<title>`:

```html
<meta name="description" content="Jenny blir 27 år. Middag på Lille Ó, lørdag 28. november 2026 kl. 19:30." />

<meta property="og:type" content="website" />
<meta property="og:url" content="https://jennyfarstad.no/" />
<meta property="og:title" content="Jenny blir 27 år" />
<meta property="og:description" content="Middag på Lille Ó, lørdag 28. november kl. 19:30. Si ifra innen 21. november!" />
<meta property="og:image" content="https://jennyfarstad.no/assets/img/og-image.jpg" />
<meta property="og:image:width" content="1200" />
<meta property="og:image:height" content="630" />
<meta property="og:locale" content="nb_NO" />

<meta name="twitter:card" content="summary_large_image" />
```

**The URLs must be absolute.** A chat app fetching your page has no page context
to resolve `assets/img/og-image.jpg` against — it needs the full `https://…`.
This is the single most common reason a preview card renders without its image.

`og:image` is already generated at `assets/img/og-image.jpg`, 1200×630. That ratio
is the de-facto standard; other sizes get cropped unpredictably by each platform.

---

## 2. The CNAME file

Create a file called `CNAME` in the repo root — no extension — containing exactly:

```
jennyfarstad.no
```

GitHub writes this file itself when you set a custom domain in the web UI. Having it
committed means the setting lives in the repo: if the Pages config is ever reset, the
domain comes back with the next push instead of silently reverting to `github.io`.

---

## 3. Enable Pages

On GitHub: **Settings → Pages**

- **Source:** Deploy from a branch
- **Branch:** `main`, folder `/ (root)`
- **Save**

Give it a minute, then confirm it works on the github.io URL *before* touching DNS.
Debugging one thing at a time beats debugging two.

---

## 4. DNS

At whoever manages `jennyfarstad.no` (Domeneshop, One.com, Cloudflare…).

**Apex domain — four A records**, all with host `@`:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Four, not one: they're redundant servers, and GitHub expects all four.

**Optional, for `www`** — a CNAME record, host `www`, value:

```
jennyfb.github.io
```

(With the trailing dot if your provider's form wants one.)

### Why apex domains need A records

A `CNAME` record cannot coexist with other records on a name, and the apex always
has `NS` and `SOA` records. So the apex can't be a CNAME, and you point it at raw
IP addresses instead. Subdomains like `www` have no such constraint. Some providers
offer "ALIAS" or "ANAME" records to work around this — if yours does, that's also
fine, pointed at `jennyfb.github.io`.

### Then

Back in **Settings → Pages → Custom domain**, enter `jennyfarstad.no` and save.
GitHub re-checks DNS. Once it passes, tick **Enforce HTTPS**.

That tickbox may be greyed out for up to an hour while a certificate is issued.
That's normal — it is not broken, it is waiting.

---

## 5. Verify

```bash
dig +short jennyfarstad.no          # should list the four GitHub IPs
curl -sI https://jennyfarstad.no    # should be 200, not 404
```

Then paste the link into a chat with yourself and confirm the preview card shows
the image and title.

**Preview caches are sticky.** Most platforms cache a URL's preview for days and
won't re-fetch on their own. Test before sending it to anyone — a bad first fetch
is hard to undo. Facebook and LinkedIn have public debugger tools that force a
re-scrape; iMessage and Signal do not.

---

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| 404 on the github.io URL | Pages not enabled, or branch/folder wrong |
| Page loads unstyled | `style.css` 404 — check the path and that it's committed |
| Custom domain "not properly configured" | DNS hasn't propagated yet; wait and re-save |
| HTTPS checkbox greyed out | Certificate still being issued; wait |
| Preview card has no image | `og:image` not absolute, or not yet reachable publicly |
| Domain works, `www` doesn't | Missing `www` CNAME record |
