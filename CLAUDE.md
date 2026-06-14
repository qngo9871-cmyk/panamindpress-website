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
- index.html      -- imprint hero + full catalogue (3 lines, 8 books)
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

## Current State (2026-06-14)
- Scaffold unzipped to /Users/user/Pana Mind Press Website/ (home folder, not iCloud).
- Quinn Path: 4 books COMPLETE — covers copied from Quinn Path Website into covers/
  (forty-three-days, between-sets, learning-to-pay-attention, morning-coffee), prices + Amazon links live.
- Quyen Ngo (The Dreaming Mind, The Night as Path): titles/bylines/buy links wired;
  covers + prices still PENDING (placeholders + TODO in index.html).
- Sage Kane (The Recognition, Blood & Leaves): titles/bylines wired; covers, prices,
  and the 2 Amazon product URLs still PENDING (buy link points to author page; TODO in index.html).
- Contact email set to hello@panamindpress.com (set up Cloudflare Email Routing to receive it).
- Domain: CNAME, sitemap.xml, robots.txt all use panamindpress.com.
- Deployed: GitHub repo qngo9871-cmyk/panamindpress-website, Pages from branch root, CNAME live.
- REMAINING for Q: Cloudflare DNS (apex A records 185.199.108-111.153 + www CNAME to
  qngo9871-cmyk.github.io, all DNS-only/grey-cloud), then enable Enforce HTTPS in Pages settings.
  Supply: 4 covers, 4 prices, 2 Sage Kane URLs.
