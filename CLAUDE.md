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

## Current State (2026-11-09)
- MEDITATION APPS section added to index.html (`<section id="apps">`, between the catalogue and the
  signup), styles in the inline <style> (`.apps`/`.app`). "Apps" link added to the primary nav on all
  3 pages (index.html#apps). Presented as "from Pana Mind Press" with no author name (pen-name rule).
  Card 1: Meditation Anchor (App Store id 6763665393, icon apps/meditation-anchor.png 240px from the
  app repo). No prices on the card (subscription prices can change; "Free to download · 7-day free
  trial" stays true).
- 2026-11-10: Card 2 Way of Insight added (app id 6832348129, approved + READY_FOR_SALE 11-10, icon
  apps/way-of-insight.png from the app's AppIcon). Way of Insight book card got a "Companion app" line
  linking to #apps. Each app card now shows 3 screenshots (apps/shots/*.jpg, 360px wide JPEGs, lazy
  loaded; .shots row pinned to card bottom via align-content:space-between). Anchor shots came from
  its US App Store listing (English set isn't in the repo); Way of Insight shots from
  ~/Projects/WayOfInsight/screenshots/final/en. Picks: Anchor idle/sit/summary; WOI home/path/check-in.
  OPEN: apps.apple.com/app/id6832348129 still 404'd on 11-10 (Apple store-page propagation lag after
  approval). Recheck; if still 404 after a day, check app availability/territories in ASC.
  Verified via headless Chrome at 1300px and true 390px (iframe).

## Current State (2026-11-08)
- DIRECT EBOOK SALES via Payhip (account qngo9871@gmail.com, store "Pana Mind Press", checkout
  connected). All 10 books are Payhip digital products: EPUB (from ~/Books Published final Kindle
  folders) + cover + description + "Send to Kindle" note, "Product is an ebook" (reduced EU VAT) on,
  Payhip prices set by Q 11-08 (USD): 43 Days 5.99, Learning to Pay Attention 3.99, Morning Coffee 4.99, Blood & Leaves 4.99, others = Kindle price. Several are below Kindle (KDP price-match risk accepted by Q). Card "Kindle $X" labels are US list prices; Blood & Leaves KDP US price is $3.99 (amazon.com.au shows A$5.57, AUD). Other labels not re-verified against KDP. None are in KDP Select.
  Product codes: 43 Days cx0Rg, Between Sets jR45K, Learning to Pay Attention 87ByN, Morning Coffee
  ePg9v, Notes from the Cushion GEh1T, Dreaming Mind nF2WO, Night as Path zjgF0, Way of Insight
  SEnm9, The Recognition 18rlI, Blood & Leaves SYjw4 (https://payhip.com/b/<code>).
- Catalogue cards: primary filled button "Buy the ebook · $X" -> Payhip; Amazon + Books2Read are a
  quiet "Or buy from ..." text line (`.book .buy-direct` / `.book .also`, inline <style>). Catalogue
  intro line now pitches direct EPUB purchase; print is Amazon-only. If a price changes on KDP,
  change it in Payhip AND the button label here.
- Payhip store About section (2026-11-09): heading "About the Press", text = shortened about.html,
  photo = brand/pana-mind-press-logo.png (800x800 wordmark render; the site has no image logo).
  Regenerate from brand/logo-source.html with headless Chrome (--window-size=800,800 --screenshot).
  Edit in Payhip store builder -> About Me section; set image via Replace -> picker -> "Choose this
  image" (closing the picker with X reverts it), then Save Changes + Publish.

## Current State (2026-11-07)
- Secondary store link is now a BOXED BUTTON matching "Buy on Amazon" (people ignored the old
  underlined text link). Label shortened to "Apple Books, Kobo & more" (uppercase via CSS). Styles
  are in the inline <style> in index.html (`.book .buy-alt`); at <=640px both buttons stretch to
  card width, centered, tighter tracking (2-up phone grid wraps the long label to 2 even lines).
  Way of Insight still has the hidden placeholder span (same class) so row alignment holds.
  Verified via headless Chrome render at 1300px and true 390px (iframe).

## Current State (2026-11-06)
- SUBSCRIBE OUTAGE FIXED: every signup failed ("Sorry, something went wrong") because the Sage Kane
  MailerLite account (login sagekane772@gmail.com, account name "Pana Mind Press") had 482 active
  subscribers vs the FREE PLAN LIMIT OF 250 (ML lowered it). ML API returned 413 "might exceed the
  current subscriber limit"; the Worker relays that as success:false. All 482 came from one CSV
  import on 2025-12-07 (scraped business list, never emailed, none from the website). Bulk-moved all
  of them to Unsubscribed (kept as records, not deleted) -> 0 active. Re-tested via the Worker:
  success:true, test address active. NOTE: the Quinn Path ML account (qngo9871@gmail.com login) is
  NOT the one the site uses. If signups fail again, check Plan usage in the Sage Kane account first.
- Welcome automation verified same day: fresh address (Gmail +alias) got "Welcome to Pana Mind Press"
  5s after signup and it arrived in Gmail; test address then unsubscribed. GOTCHA: re-subscribing an
  EXISTING address only restores it (no group re-join) so the welcome email does NOT re-send — always
  test with a brand-new address. Active subscribers now 1 (qngo8@yahoo.com) of 250.

## Current State (2026-06-20)
- 10th book added — Quyen Ngo, "Way of Insight" (Buddhist Studies line). Kindle $3.99
  (ebook; paperback price TBD), Amazon ASIN B0H656DTQJ. Cover covers/way-of-insight.jpg.
  No reviews yet so no star rating shown. NO Books2Read/D2D link yet — the card has an
  INVISIBLE buy-alt placeholder (`<span class="buy-alt" ... visibility:hidden>`) reserving
  the "Also on Apple Books, Kobo & more" line so the Buy button aligns; swap it for the
  real `<a>` once the D2D universal page exists (TODO comment is on the card in index.html).
- ALL 10 COVERS NORMALIZED to 776x1200. Previously off-standard: way-of-insight (749),
  morning-coffee (811 — the old "1025x1200 near-square" note is now STALE), the-recognition
  (847), blood-and-leaves (847). Off-standard aspect ratios render at different heights in a
  row (the CSS frame's aspect-ratio:2/3 acts as a floor, not a hard clip — narrower covers
  overflow taller, wider ones stay shorter), which made rows look uneven. Fixed by trimming
  side margins to 776x1200 (center-crop, no title text lost). RULE: every new cover must be
  exactly 776x1200 or it will be uneven next to the others.
- CSS alignment reserves (css/style.css): `.book .sub { min-height: 4.1rem }` (3 lines) and
  `.book h3 { min-height: 2.36em }` (2 lines) so bylines/prices/buttons line up across a row
  regardless of how many lines each title/subtitle wraps to. Buy button uses margin-top:auto
  (bottom-anchored), so every card needs a buy-alt line (real or the hidden placeholder).
- Verified even via headless Chrome render + per-column text-row measurement (all 3 rows).

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
