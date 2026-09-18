# Reggae Pot Jamaican Grill — Redesign Prototype B ("Market Gold")

**Built:** September 17, 2026 · **Status:** Coded prototype, homepage only, not connected to WordPress
**Files:** `index.html` + `assets/site-b.css` + `assets/` (same real photos/video/logo as Prototype A, copied into this folder so it stands alone). Open `index.html` directly in a browser.

> **Why this exists:** Cynthia asked for a second, genuinely different design so the client has an actual choice, not two versions of the same layout. This sits alongside [`06-Redesign-Prototype`](../06-Redesign-Prototype/) ("Prototype A") — both fix the same Sep 3 audit findings (broken hero, buried order CTA, no menu content), with different visual systems.

---

## How this is actually different from Prototype A, not just recolored

| | Prototype A | Prototype B (this one) |
|---|---|---|
| **Header** | Cream background | **Gold background** — matches the live site's actual nav bar color, which A doesn't use |
| **Hero mechanic** | Full-bleed photo/video, centered text over a dark scrim | **Split panel** — solid gold text block + photo/video side by side, no scrim needed |
| **Primary CTA color** | Gold buttons | **Red buttons** — a real brand hue A leaves as a minor accent only |
| **Section order** | Hero → Good Vibes → Dishes → story sections → Locations (near the bottom) | **Hero → Dishes → Locations** moved up right after the hero (the Sep 3 audit calls the menu the highest-intent content), story sections after |
| **Story sections (Good Vibes, Jamaican Grill, Flavors, Specialties)** | Side-by-side photo card + text | **Stacked** — photo full-width on top, text centered below |
| **Why/Tamara section** | Two-column, vertical trait list, gold background hero-style card | **Gold full-width band**, circular portrait, traits as a horizontal row |
| **Ending** | Final CTA on a gold gradient with a photo card | **Solid ink-black band** — bookends the gold hero with the opposite end of the palette instead of repeating gold |
| **Dish cards** | Dark green section, uniform gradient-tinted photos | **Cream section**, white cards with black outline, a red "Bestseller" ribbon on Oxtail |

Both use the same real assets, same real brand colors (`#0b9444` green, `#ffbf00` gold, `#b50d0a` red, pulled live from the site), same Fraunces/Work Sans font pairing, and the same live-site-verbatim copy blocks — this is a genuinely different visual system built from the same real material, not a reskin.

## What's identical on purpose (not overlooked)

- Every live-site content block (Good Vibes, Jamaican Grill/About Us, Flavors of Jamaica, Jamaican Specialties, Order Online) carries the same near-verbatim text as Prototype A, including the same corrected Centennial Sunday hours and the same punctuation fixes from the em-dash cleanup round.
- Every section has both "Order Online: Centennial" and "Order Online: Denver" buttons, from the start this time (not added in a later pass like Prototype A).
- No em-dashes anywhere in visible content, verified the same way as Prototype A's cleanup (checked `document.body.innerText`, not just the source).
- Mobile sticky order bar, scroll-reveal animation, and video pause-on-scroll all carried over.

## Trimmed for the new layout (flagging, not hiding)

The Why/Tamara trait descriptions are shortened in the horizontal trait-row layout (e.g. "Rooted" drops the "The proper names, every time" line) since four full paragraphs don't fit a tight horizontal row the way they fit a vertical list in Prototype A. This is original site copy, not one of the live-site-verbatim blocks, so trimming it for a layout that needs shorter chunks is a design call, not a content accuracy issue — but it's a real difference worth knowing about if this design gets picked.

## Verified

- ✅ Zero em-dashes in visible content (checked via `document.body.innerText`)
- ✅ All 12 content sections confirmed to have both Centennial and Denver order links (DOM query)
- ✅ All 4 dish cards, all 4 review cards, all 4 story-section photos confirmed loading the correct real asset (checked `background-image` values)
- ✅ Section background colors confirmed matching the intended palette (computed styles): red quick-strip, cream dishes, cream-deep locations, gold Why, red Order Online, ink-black Final CTA, dark-red footer
- ✅ Zero console errors
- ✅ Screenshot-confirmed the hero renders correctly (gold panel + photo, no gap, both CTA buttons visible)
- ❓ **Could not get a screenshot past the hero this round** — the Browser tool's screenshot returned blank/timed out on every attempt after scrolling, the same recurring flakiness documented throughout this whole project. Every section's structure and content is confirmed correct via the checks above, but **please open `index.html` yourself and scroll through the full page** before treating this as visually final — I have not personally seen the Dishes, Locations, Why, Reviews, or Final CTA sections rendered, only verified their underlying code.

## Revised September 17, 2026 — dead space in the Dishes header row

Cynthia's screenshot showed a big empty box to the right of "The dishes people come back for," at wider screen widths.

**Root cause:** `.dishes-head`'s two children (the text block and the button group) both sized to their own content only. At a wide desktop width, `text width + button width` was slightly more than the row could fit, so instead of sitting side by side they wrapped onto their own lines, both left-aligned — leaving the entire right two-thirds of the row empty.

**Fix:** gave the text block `flex:1 1 320px` so it grows to fill whatever space is left next to the (fixed-width) button group, instead of only taking its own content width. Now the two sit on one row spanning the full width at any screen size, and only wrap to stacked on genuinely narrow screens where there isn't room for both.

**Verified:** ✅ confirmed via `getBoundingClientRect` at a 1600px-wide viewport — the text block and button group now sit side by side spanning the full 1132px row width (previously both stacked left, leaving ~450px of empty space on the right). Zero console errors. ❓ Could not get a screenshot confirming this visually this round (same recurring Browser-tool flakiness) — the measurement is unambiguous, but take a look yourself.

## Revised September 18, 2026 — applied Brian's standing design requirements

Same audit as Prototype A, against Brian's (CEO) standing requirements for every Magister restaurant redesign:
1. Visible Home nav link
2. "Contact" not "Contact Us" — n/a, no Contact link here
3. No cursive fonts — ✅ already compliant
4. **Order Online CTA prominent, same button color throughout**

**What was wrong:** the primary button was red almost everywhere, but the header had Centennial as outline and Denver as the solid one (reversed from every other section), and the Order Online + Final CTA sections both used gold instead of red — because their dark/colored backgrounds meant red on top of it looked wrong or invisible.

**Fixed:**
- Added a **Home** link, first item in the nav.
- Fixed the header to match the sitewide pattern: Centennial solid red, Denver outline.
- Final CTA (ink background): button now uses the same red as everywhere else — red always contrasted fine there, it just hadn't been changed back.
- Order Online: this was the real conflict — its background was solid red, so a red button on top of it would vanish. Rather than give the button a special color just here, the **section's background changed to dark green instead** (a tone not used anywhere else in this prototype, so it still reads as its own distinct section, and doesn't blend into the ink-black Final CTA next to it). The button itself is now the exact same red as every other Order Online button on the site.
- Removed the now-unused `.btn-gold` CSS rule.

**Flagging, not changing without your say-so:** Brian's CRO notes also flag "No Wait" as an unsupported promise — this prototype's hero and Order Online sections both use that exact phrase, which you explicitly asked for earlier this session. Didn't touch it without checking with you first.

**Verified:** ✅ all 13 primary buttons confirmed resolving to the exact same red via computed styles, Order Online's new background color confirmed, zero console errors.

## Revised September 18, 2026 — periods in headings

Same fix as Prototypes A and C: removed the trailing/internal periods from every `<h1>`/`<h2>` (hero, Locations, Why/Tamara, Final CTA) — flagged separately from Brian's 4-point list, as item #1 on Beth's earlier list of AI-design tells.

**Verified:** ✅ zero periods remain in any heading, confirmed via `textContent`, zero console errors.

## Not done yet

- The menu page (`/menu/`) — Prototype A has one built; this prototype doesn't have its own yet. If this direction gets picked, the menu page would need the same gold/red treatment applied.
- Not published anywhere yet (Prototype A is live at Cynthia's GitHub — this one is local-only pending her review).
- Same outstanding items as Prototype A: the other 6 pages, WordPress implementation, named/attributed review quotes, hero video compression.
