# Pana Mind Press Website

Imprint website for Pana Mind Press. Static HTML/CSS site, published via GitHub
Pages with a custom domain (CNAME). Books-first catalogue: presents titles
grouped by publishing line, with author names as bylines that link OUT to each
author's own home (Quinn Path -> quinnpath.org; Sage Kane / Quyen Ngo -> their
Amazon author pages). 

## Critical editorial rule
The three pen names (Quinn Path, Sage Kane, Quyen Ngo) must NEVER be presented
as the same person. No shared bios, no author photos on this site, no language
implying common authorship. They are three distinct authors published by one
press. Keep copyright footer as "Pana Mind Press", never a personal name.

## Stack
- Static HTML / CSS / JavaScript (no framework, no build step)
- GitHub Pages hosting; .nojekyll present so all files serve as-is
- CNAME set to panamindpress.com (registered at Cloudflare)

## Structure
- index.html      -- imprint hero + full catalogue (3 lines, 9 books)
- about.html      -- about the press (imprint only, no authors)
- contact.html    -- single imprint contact address
- css/style.css   -- house style (intentionally NOT the Quinn Path look)
- covers/         -- book cover JPGs (see covers/README.md for exact filenames)
- sitemap.xml, robots.txt -- SEO (replace REPLACE-WITH-DOMAIN after domain set)

## Outstanding TODOs (search the code for "TODO")
- Add 4 covers: dreaming-mind, night-as-path, the-recognition, blood-and-leaves
  (Quinn Path's 4 covers also need copying from quinnpath.org into covers/)
- Add prices for the 4 non-Quinn-Path books
- Add Amazon product URLs for the 2 Sage Kane books (currently point to author page)
- Set imprint contact email in contact.html
- Set domain in CNAME, sitemap.xml, robots.txt

## Deploy (GitHub Pages)
1. Create repo, push these files.
2. Settings -> Pages -> deploy from branch (root).
3. Add CNAME file containing the apex domain; set DNS A records to GitHub Pages
   (185.199.108-111.153) + www CNAME to <user>.github.io. Enforce HTTPS.

## Instructions for Claude Code
At the end of every session, update this Current State section to reflect progress.

## Current State (2026-06-17)
- SUBSCRIBE FORM FIX: the form no longer posts to the MailerLite jsonp endpoint. That endpoint
  forced double opt-in (baked into the form, unchangeable via API or the new UI) and its
  confirmation emails were never delivered, so signups died silently. The form now POSTs (multipart,
  field `email` + `website` honeypot) to a Cloudflare Worker `pmp-subscribe`
  (https://pmp-subscribe.qngo9871.workers.dev), which calls the MailerLite API to add the subscriber
  as `active` to the "Pana Mind Press" group — welcome automation fires immediately, no confirmation
  step. Worker source + deploy.sh live in /Users/user/panamindpress-subscribe-worker/ (not in this
  repo). ML key is the Worker's `ML_TOKEN` secret. CF deploy token: ~/.cloudflare/panamindpress-workers.token.
  Success copy updated to "You're subscribed…". Verified end-to-end (active signup + welcome email).

## Current State (2026-06-15, later)
- Readability pass: darkened the three ink tones (final --ink #141209, --ink-soft #2b2920,
  --ink-faint #312e23) and bolded the small uppercase labels (kicker/eyebrows/colophon/section
  nums/bylines -> font-weight 600, tighter tracking). The faint #8b8678 labels were unreadable.
- Amazon ratings updated on catalogue cards: 43 Days of Fire 4.6 (31), The Recognition 4.6 (26),
  Morning Coffee 5.0 (2), Blood & Leaves 5.0 (3), The Dreaming Mind 5.0 (1),
  Learning to Pay Attention 5.0 (1). Notes from the Cushion already 5.0 (1).
  Between Sets + Night as Path have no reviews yet (no rating shown). All pushed + live.

## Current State (2026-06-15)
- 9th book added — Quinn Path, "Notes from the Cushion and the Kitchen Table" (Kindle $4.99 /
  Paperback $13.99), cover at covers/notes-from-the-cushion.jpg (RGB 776x1200).
- Newsletter migrated Web3Forms -> MailerLite. Subscribe form posts client-side to MailerLite
  jsonp endpoint (account 1967807 "Sage Kane", form 190283260541011131, group "Pana Mind Press",
  double opt-in ON). Sending domain panamindpress.com authenticated (DKIM CNAME + merged SPF +
  verification TXT + DMARC, all in Cloudflare). Welcome automation live; sender + account company
  name set to "Pana Mind Press" <hello@panamindpress.com> (never Sage Kane — pen-name rule).
  Quinn Path uses a SEPARATE MailerLite account (2211845). API key: ~/.mailerlite/api.token.
- Availability: about.html + catalogue note say ebooks are also on Apple Books/Kobo/B&N/etc.;
  every catalogue card has a per-book "Also on Apple Books, Kobo & more" Books2Read link
  (books2read.com/u/CODE, ebooks wide via Draft2Digital). Codes verified live in index.html.
- Outstanding: NOTHING.

## Current State (2026-06-14)
- Scaffold unzipped to /Users/user/Pana Mind Press Website/ (home folder, not iCloud).
- CATALOGUE COMPLETE — all 8 books have cover + USD price + real Amazon product link:
  - Quinn Path: forty-three-days, between-sets, learning-to-pay-attention, morning-coffee.
  - Quyen Ngo: dreaming-mind ($7.99), night-as-path ($7.99).
  - Sage Kane: the-recognition ($4.99), blood-and-leaves ($2.99) — product links wired.
- REDESIGN (2026-06-14): rebuilt css/style.css as a cover-forward literary house style —
  large covers in a centered flex gallery, Fraunces (display) + Spectral (body) + Inter
  (labels) via Google Fonts (links in all 3 HTML heads), stronger line dividers, refined
  hero/footer, hover states, responsive 3-up/2-up. Covers use object-fit:cover @2/3.
  NOTE: morning-coffee.jpg is near-square (1025x1200) so it crops at the sides in the 2/3
  frame — acceptable but a true 2:3 cover would sit better.
- COVERS OPTIMIZED via Pillow: all -> RGB, max 1200px, q80, stripped metadata, progressive.
  Total 7.5MB -> 1.2MB. morning-coffee was CMYK+ICC (wrong colors in some browsers) -> RGB.
- Contact email set to hello@panamindpress.com (still need Cloudflare Email Routing to receive it).
- Domain: CNAME, sitemap.xml, robots.txt all use panamindpress.com.
- Deployed: GitHub repo qngo9871-cmyk/panamindpress-website, Pages from main/root, CNAME live.
  Live over http://panamindpress.com (www -> apex).
- DNS DONE via Cloudflare API (token saved at ~/.cloudflare/panamindpress-dns.token, chmod 600,
  zone a58c37d3cc90fbe26000e02b90bb7afd): 4 apex A (185.199.108-111.153) + www CNAME to
  qngo9871-cmyk.github.io, all DNS-only. Resolves correctly via 1.1.1.1.
- HTTPS LIVE: cert issued (after a domain remove/re-add nudge — it had stalled ~2h); Enforce HTTPS ON.
  https://panamindpress.com (200), http -> 301 https, www -> apex.
- Subscribe form: Web3Forms (client-side FormData fetch + honeypot, key in index.html);
  shows in-page confirmation/error message under the form; notifications -> hello@/Gmail. WORKING + verified.
  (Inline <script> must stay valid JS — a stray }); once broke it and made the form do a default
  submit/page-jump; node --check the script before shipping.)
- Email Routing LIVE (hello@ -> Gmail). Morning-coffee cover fixed (2:3).
- HTTPS verified: Let's Encrypt cert approved, https_enforced=true, http->https. NOTHING outstanding.
