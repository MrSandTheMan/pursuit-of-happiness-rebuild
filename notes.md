# Pursuit of Happiness Realty — Rebuild Notes (2026-09-21)

## What was built
Self-contained static recreation of pursuitofhappinessrealty.com, modernized.
Output: `~/workspace/pursuit-of-happiness-realty/rebuild/`

## Page mapping (old → new)
| Original URL | New file | Notes |
|---|---|---|
| `/` (Home) | `index.html` | Hero, discount band, 3 listing cards, About, testimonials placeholder, contact |
| `/bedrooms` | `listings.html` | Sold Kauneonga Lake spotlight + MLS search form |
| `/gallery` | `gallery.html` | Welcome, YouTube embed, photo gallery |
| `/list` | `tips.html` | Buyer/seller tips, renumbered, typos fixed |
| `/page-take-a-look` | `new-listing.html` | 109 So. Main teaser |
| `/idx/wrapper` | `mls-search.html` | MLS search landing page linking out to live OneKey MLS feed |

Nav labels were modernized for clarity: "Bedrooms" → "Listings", "List" → "Buyer & Seller Tips",
"Page take a look" → "New Listing", "More" (dead dropdown) removed. "Search the MLS" added as CTA.

## Modernization fixes (from scan notes)
- Dead `#` links: all removed. "More" empty dropdown dropped; every CTA now points somewhere real.
- Typos fixed: "Seach" → "Search", "commision" → "commission", "Kauneouga" → "Kauneonga", "alot" → "a lot".
- Footer © 2025 → © 2026.
- Kauneonga Lake $370K listing shown with a **Sold** badge (it was marked sold on the original).
- Added About section (facts only: Elliott, Liberty NY, service area) and a Testimonials section built as
  clearly-marked placeholders — no invented quotes, stats, or claims anywhere.
- Alt text added to every image. Semantic headings, responsive nav, mobile layouts.

## Images
Downloaded from the original site's wsimg CDN and optimized (max 1400–1600px, q78):
`hero.jpg` (original hand-drawn flyer — used in About), `listing-red1/2/3.jpg` (Wade Rd house),
`scott-outside.jpg` (Kauneonga Lake sold house), `stock.jpg` (gallery only).
- `blob-3830ca7.png` / `blob-f798686.png` (logo marks) downloaded as **pure black** — unusable;
  replaced with a text wordmark. Noted for the owner: supply a real logo file.
- `IMG_4209(1…` (109 So. Main photo) had a truncated URL and returned 0 bytes — that card and the
  20-acre / Youngsville cards use tasteful labeled placeholders until real photos are supplied.

## Contact form
Front-end only. Submit shows an honest notice ("not connected to an inbox yet") and points to the
phone/email. **Before going live:** wire the form to Formspree, Netlify Forms, or the owner's email
handler — see the `form-note` in `index.html`.

## MLS integration
Not replicated — the rebuild links out to the live OneKey MLS Matrix portal at the same IDX URLs
from the original site (`idx=6e2d31e`). The Listings page search form is a criteria picker whose
"Search Now" opens the live IDX search portal in a new tab.

## Design calls
- Palette: warm paper + ink + barn-red accent (echoes the red-roof listing photos and the folk-art flyer).
- System font stacks only — zero external requests except the YouTube embed and outbound MLS links.
- All pages work from `file://`; shared stylesheet at `assets/styles.css`.
- Testimonial placeholders are visually dashed/gold-labeled so the owner knows to fill them in.

## Verification
- All internal links resolve; every `<img>` src exists and is non-empty; no bare `#` links.
- Contrast: all text pairs ≥ 4.5:1 WCAG AA (one gold-on-white note darkened from #a97e2c to #6e5218 to pass).
- Screenshots: desktop (1400px) + mobile (390px) for all 6 pages, rendered in headless Chrome —
  0 broken images, 0px horizontal overflow on every render.
- Issues found and fixed during verification:
  1. Nav "Search the MLS" CTA was unreadable (white text on light pill) when on the MLS page —
     fixed with a dedicated `.nav-cta.active` style (dark red pill, white text).
  2. Two lazy-load false positives for `hero.jpg` in the first automated check — confirmed the file
     decodes fine in Chrome; the flags were just images not yet fetched below the fold.
- Note: the gallery's YouTube iframe shows an error tile in the offline sandbox only; it is the one
  sanctioned external embed and will load in a normal browser with internet access.
- Screenshot set kept at `/tmp/poh-shots/` (12 PNGs) for reference.

## Still needed from the owner (Elliott)
1. Real logo file (the originals downloaded black).
2. Photos for: 20-acre Bethel Woods parcel, Youngsville $319K property, 109 So. Main listing.
3. Real testimonials to replace placeholders.
4. Form endpoint wiring before launch.
5. Confirm whether the 109 So. Main listing is still "coming soon" or now live.

## Update (2026-11-07) — Elliott's photos
- Elliott emailed 5 photos on Nov 4, 2026 ("Okay", elliottpursuit@gmail.com, "I'll send a few pictures now and later"). Originals saved in `elliott-photos/` (image0-4.jpeg, 640x480).
- All 5 show the same wooded property (dark siding, red trim, deck, fire pit, red barn). Elliott did not label them. Placed on the Youngsville listing ("3 Houses on 4 Acres", $319,000) as the only multi-structure property in the build; the Bethel Woods land parcel and 109 So. Main placeholders are untouched. If Elliott meant them for another listing, move them.
- Rotation: image2, image3, image4 arrived sideways; rotated 90 degrees clockwise and verified upright. image0 (barn) also arrived sideways but was missed on the first pass; visual QA caught it, rotated 90 degrees clockwise and re-uploaded.
- Files in `rebuild/assets/`: `youngsville-house.jpg` (image1, main house front, used on the homepage card), `youngsville-cabin.jpg` (image4), `youngsville-barn.jpg` (image0), `youngsville-deck.jpg` (image2), `youngsville-deck2.jpg` (image3). All 5 also added to `gallery.html`.
- Published to GitHub Pages: https://mrsandtheman.github.io/pursuit-of-happiness-rebuild/ (repo MrSandTheMan/pursuit-of-happiness-rebuild). Preview only; production site untouched.

## Update (2026-11-07, round 2) — text balance, grouping, links, flyer rotation
- Flyer (assets/hero.jpg) was sideways: the hand-drawn flyer was scanned rotated 90 degrees, text running vertically. Rotated 90 degrees clockwise, trimmed the white scan margins (1600x2227 portrait to 1903x1549 landscape). All text now reads left to right. Original saved as `hero-original.jpg` in the project folder (not shipped).
- Text balance (Socrates lesson, now a standing SOP rule): added `h1,h2,.lede{text-wrap:balance}` and `p{text-wrap:pretty}` to assets/styles.css. QA checks every heading/lede for the five-words-then-one-orphan pattern at desktop and phone width.
- Gallery grouped by property (new SOP rule): Wade Road (3), Kauneonga Lake (1), Youngsville (5), More from Pursuit of Happiness (stock + flyer), each under its own heading with a short note.
- Link check (Nov 7): every internal file exists, #contact anchor present, MLS IDX links 200, Facebook 200 (login redirect is normal logged-out behavior), YouTube embed 200, Google Maps 200 with a browser user agent (403 to bare curl is bot-blocking, not a broken link).
- SOP: ad-landing-page-sop.md Sections 5 (photo grouping), 7 (QA gate), 10 (run sheet), 11 (standing balance rule) updated; Drive copy synced in place and verified byte-identical Nov 7.
- QA round 2 (Nov 7) found two more defects, fixed same day: the gallery flyer tile cropped the website line (fixed with a `figure.fit` no-crop rule) and two card titles still orphaned (balance guard extended to h3, .card-title, figcaption). Phone-width balance verified by width simulation with DejaVu proxies (card titles 2/4, 4/3, 3/3; h1 4 lines ending "Upstate New York."), not a real phone render.

## Re-verification (2026-09-22)
- All six pages present; all `src=` references resolve to existing files (no broken images).
- Homepage rendered in headless Chrome at 1400×900: header/nav, hero image, CTAs, and discount band all display correctly.
- 109 So. Main image (`IMG_4209`) again returned 0 bytes from the CDN (truncated URL on the original) — placeholder retained.
- Nothing published; build remains local and unpublished, awaiting Sandy's review.
