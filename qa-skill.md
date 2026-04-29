# Wix Page QA Skill

Check the page. Catch what's broken. Give the PMM a clear, actionable QA sheet.

---

## Before You Start — Collect These From the PMM

Ask the PMM to provide all of the following before you begin:

**Links:**
1. **Mockup URL** — the staging/preview URL of the built page
2. **Content doc link** — Google Doc with the approved copy
3. **Figma link** — the final approved design file

**Team (for the QA sheet header):**
4. **PMM name** — who requested the QA
5. **SEO Manager name**
6. **Content owner name**
7. **Design owner name**
8. **Tech design owner name**

Do not start the QA until you have all 7 inputs.

---

## QA Basics

| Layer | What You're Checking |
|-------|---------------------|
| **Content** | Does every word on the page match the content doc exactly? Any typos? Does SEO metadata match? |
| **Design** | Does the page look like the Figma file (layout, typography, colors, images)? |
| **Visual / Behavior** | Are there bugs, broken elements, or behavioral issues? |

Each issue found becomes one row in the QA sheet.

**The content doc is the sole authority for all copy.** The Figma file is used for design and layout checks only — never for verifying text. If the Figma shows different copy than the content doc, the content doc wins.

---

## Step 1: Content Check (Page vs. Content Doc)

Open the content doc and the live page side by side. Go section by section, top to bottom:

- [ ] Hero headline and sub matches content doc exactly
- [ ] Every fold's headline and body copy matches
- [ ] CTAs match (exact wording, placement)
- [ ] Legal disclaimers, fine print match
- [ ] No extra text on the page that isn't in the doc
- [ ] No missing text or folds from the doc that should be on the page
- [ ] Capitalization matches (title case vs. sentence case as specified)
- [ ] Punctuation matches — including periods at the end of taglines, send-offs, and short phrases
- [ ] No spelling errors or typos anywhere on the page
- [ ] No doubled words or duplicated text blocks
- [ ] **Alt text matches content doc** — for every image that has a specified alt text in the content doc, confirm it matches exactly. Run the alt text JS check in Step 3b to pull all image alts at once. Log mismatches as content issues.
- [ ] Send-off / closing line is complete and punctuated correctly
- [ ] **SEO Title:** Confirm the page title matches what the content doc specifies
- [ ] **SEO Meta Description:** Confirm the meta description matches the content doc exactly

**Log every discrepancy as an issue. Even one wrong word, missing period, or typo is an issue.**

---

## Step 2: Design Check (Page vs. Figma)

Design check covers visual layout, typography style, colors, images, and spacing ONLY. Do not use Figma to verify copy.

**How to access Figma:**

**Option 1: Figma MCP tools (try first)**
Parse the Figma URL — do not open it as a browser link:
- From `https://figma.com/design/AbCdEfG/FileName?node-id=1-2`
- `fileKey` = `AbCdEfG`
- `nodeId` = `1:2` (replace `-` with `:`)

Run `get_metadata` to get the file structure, then `get_design_context` on each frame for a screenshot and design details.

**Option 2: PNG export (fallback)**
Ask the PMM: "The Figma file is not accessible from my session. Please export the approved frames as PNG — one per fold/section — and share them here."

**Never skip the design check.**

Check each fold:

**Typography:**
- [ ] Font matches (family, weight, size)
- [ ] Font color matches
- [ ] Line height and letter spacing feel right
- [ ] Text alignment matches (left/center/right)

**Layout:**
- [ ] Spacing between elements matches
- [ ] Section order matches Figma
- [ ] Column layout matches (2-col, 3-col, etc.)
- [ ] Container widths match
- [ ] **Sub line count consistency:** If all card subs in a fold are 2 lines and one card goes to 3 lines, flag it.

**Images & Media:**
- [ ] Correct image is used (not a placeholder)
- [ ] Image matches the Figma — flag wrong asset
- [ ] Image aspect ratio matches Figma
- [ ] Image is not pixelated or blurry
- [ ] Videos/animations are present and playing
- [ ] Images in carousels or scrollable sections are not cut off. Scroll through all items on both desktop and mobile.
- [ ] **Text on images (ALL folds):** Read all text inside any image across the entire page — UI screenshots, product mockups, calendar previews, app screens, feature fold illustrations, booking examples. Apply to every fold with an image that has visible text inside it. Do not limit to template cards.
- [ ] **Alt text in scrollable sections:** Scroll through ALL items in every carousel/scrollable section (not just visible on load). Check each image has accurate alt text.

**Colors & Styles:**
- [ ] Background colors match
- [ ] Button colors and styles match
- [ ] Icon colors match
- [ ] Border radius, shadows match

**CTAs & Buttons:**
- [ ] Button style matches Figma
- [ ] Button position matches
- [ ] Hover state looks correct (if visible)
- [ ] **Hero CTA visible above the fold WITHOUT scrolling** — both desktop and mobile
- [ ] **Each fold that should have a CTA has one visible**

---

## Step 3: Visual & Behavioral Issues

**Text Issues:**
- [ ] Double spaces between words
- [ ] Widows (single word on last line) in important headlines
- [ ] Text that is cut off or overflowing its container
- [ ] Text rendering twice (duplicated content blocks)

**Link Issues:**
- [ ] Links that look like links but are not clickable
- [ ] Underlined text that is NOT a link
- [ ] Links opening in wrong tab
- [ ] **404 check:** Click every visible link and CTA. Flag any that return a 404 — launch blocker.
- [ ] **Destination check:** For every link with a URL specified in the content doc, confirm it lands on the correct URL. Flag mismatches (expected vs. actual URL in the How to Fix column).
- [ ] **Inline anchor check:** When the content doc specifies a particular word/phrase should be hyperlinked, verify that exact word is actually clickable on the page — not just that the URL is reachable.

**Images:**
- [ ] Images that look pixelated or stretched
- [ ] Images that fail to load (broken placeholder)

**Scroll & Overflow:**
- [ ] No horizontal scroll on desktop (unless intentional carousel)
- [ ] Horizontal scrollable sections let the user reach the last item
- [ ] Sticky headers not blocking content

**Interactive Folds (Accordions, Tabs, Carousels, etc.):**
- Note which fold and what type. Flag for PMM to manually test behavior.

---

## Step 3b: SEO Technical Checks

Run these via `javascript_tool` in the browser. All are readable from the live DOM.

**OG tags:**
```js
[...document.querySelectorAll('meta[property^="og:"]')].map(m => m.getAttribute('property') + ': ' + m.getAttribute('content'))
```
Confirm `og:title`, `og:description`, `og:image`, `og:image:width`, `og:image:height`, `og:site_name` are all present. Flag any missing.

**Schema markup:**
```js
[...document.querySelectorAll('script[type="application/ld+json"]')].map(s => s.textContent)
```
Flag if none present. Log the type found — SEO Manager confirms it is the correct type.

**External link rel attributes:**
```js
[...document.querySelectorAll('a[href]')].filter(a => a.hostname !== location.hostname && a.rel).map(a => a.href + ' → rel=' + a.rel)
```
Flag external links with `noopener` or `noreferrer` if the SEO spec requires link equity to pass.

**Image filenames:**
```js
[...document.querySelectorAll('img')].map(i => i.src.split('/').pop())
```
Flag generic filenames (e.g., `image1.jpg`) if the SEO spec requires descriptive filenames.

**Hero image format/size:**
Check hero image `src` extension — flag if `.jpg` or `.png` instead of `.webp` or `.avif`. Use `fetch(src, {method:'HEAD'})` to get `content-length` — flag if over 200KB.

**Alt text (all images):**
```js
[...document.querySelectorAll('img')].map(i => ({src: i.src.split('/').pop(), alt: i.alt}))
```
Compare each alt against the content doc. Flag: (1) missing alt text, (2) alt text that does not match the content doc exactly. Scroll through carousel sections first to load all items.

---

## Step 4: Mobile Check

Repeat Steps 1–3 on mobile view (320px–375px width).

- [ ] Text is readable without pinching
- [ ] Buttons are large enough to tap (min 44px)
- [ ] Nothing is cut off on the right edge
- [ ] Images stack correctly
- [ ] Images in carousels not cut off or cropped on mobile — scroll through all items
- [ ] Navigation/hamburger menu works (note for PMM to test on device)
- [ ] CTAs visible above the fold on mobile
- [ ] No horizontal scroll on mobile
- [ ] Spacing feels proportional

---

## Step 5: Manual Checks for PMM

**Note on links:** Links with a specified URL in the content doc are verified in Step 3. Only links with NO specified URL go here.

**The PMM must manually verify:**
1. Links where the content doc does not specify a destination URL
2. All interactive element behaviors (accordions, carousels, search forms, template cards)
3. Mobile behavior on a real device
4. Analytics: for each CTA and interactive element, confirm (a) the click event fires, (b) each event has a unique, distinct name — two CTAs on the same fold must not share the same event name, (c) no CTA is missing an event entirely
5. SEO meta description in page head (exact match to content doc)
6. Schema markup correctness — SEO Manager confirms the schema type found in Step 3b is correct for this page

---

## Output: The QA Sheet

**Every QA session produces TWO outputs — both are required:**

1. **Markdown file** — saved to `O-output/[page-name]-qa/qa-sheet.md`
2. **Google Sheet** — created from the same content, link shared in chat as a plain URL

### QA Sheet Header

```
PAGE QA REPORT
==============
Mockup URL:      [staging/preview URL]
Page URL:        [final URL from content doc]
QA Date:         [today's date]

Google Sheet:    [link — add after sheet is created]

Team:
  PMM:           [name]
  SEO Manager:   [name]
  Content:       [name]
  Design:        [name]
  Tech Design:   [name]
```

### Issues Table

| # | Requested By | Desktop / Mobile | Issue | How to Fix | Screenshot | Fixed by tech design | Approved | Comments |
|---|---|---|---|---|---|---|---|---|

**Issue column:** SHORT — location and problem name only. Example: "Fold 8, loyalty program sub — wrong wording."
**How to Fix column:** Full detail, including exact replacement copy.

```
Bad:  "Fold 8: page says 'they make on', content doc says 'made on'."
Good: "Fold 8, loyalty program sub — wrong wording."
Fix:  "Change 'they make on' to 'made on'."
```

### Manual Checks Table

| # | What to Check |
|---|---------------|
| 1 | CTAs: Confirm all buttons link to the correct destination. Confirm click events fire. |
| 2 | Links: Confirm all inline and text links navigate to the correct URLs. |
| 3 | Interactive elements: Test [list specific elements found on this page]. |
| 4 | Mobile: Test hamburger menu and all interactive elements on a real device. |
| 5 | Analytics: Each CTA must have a unique event name. Verify no two CTAs on the same fold share an event name, and no CTA is missing an event. |
| 6 | SEO: Confirm meta description in page head matches content doc exactly. |
| 7 | SEO (Schema): Confirm the schema type found in Step 3b is correct for this page. |

### Google Sheet Delivery (MANDATORY)

1. Write a CSV to `/tmp/qa-sheet-full.csv` using Python's `csv` module with `quoting=csv.QUOTE_ALL`
2. Base64 encode: `base64 -i /tmp/qa-sheet-full.csv` (macOS — `-i` flag required)
3. Upload via Google Drive MCP `create_file` with `mimeType: text/csv`
4. Share the link in chat as a plain URL:

```
QA sheet delivered. Here is your Google Sheet with all issues and manual checks:

https://docs.google.com/spreadsheets/d/[FILE_ID]/edit
```

The link must be a plain URL. Do not embed it in markdown. Do not skip this step.

---

## Quality Checklist (Before Delivering)

- [ ] All 7 inputs collected before starting?
- [ ] Every section checked against the content doc?
- [ ] Typos, spelling errors, missing punctuation checked?
- [ ] SEO title and meta description checked?
- [ ] Design checked against Figma?
- [ ] Visual and behavioral issues checked?
- [ ] Every link clicked — 404s checked?
- [ ] Link destinations checked against content doc URLs?
- [ ] Inline anchor links verified (specific words actually hyperlinked)?
- [ ] Text inside ALL images across ALL folds read?
- [ ] All carousel/scrollable sections scrolled through — alt text on every item checked?
- [ ] Sub line count consistency checked within each fold?
- [ ] Step 3b SEO JS checks run (OG tags, schema, rel attributes, image filenames, hero image)?
- [ ] Mobile view checked?
- [ ] Manual checks table only contains links with no specified URL in content doc?
- [ ] Analytics manual check specifies distinct event names per CTA?
- [ ] Issue column short — location and problem name only?
- [ ] How to Fix column has full detail including exact replacement copy?
- [ ] Google Sheet created and link shared in chat as plain URL?
- [ ] Google Sheet link added to md file header?

---

## Common Issues to Watch For

**Content:**
- Hero headline doesn't match content doc (often updated in doc after build started)
- CTA button text differs from content doc by one word
- Missing legal text at bottom of page
- Send-off or tagline missing final period
- FAQ answer text differs from content doc in small but real ways (copy drift during dev)

**Design:**
- Font weight is Regular instead of SemiBold
- Section background color slightly off
- Mobile image is the desktop image squeezed (wrong asset)

**Visual/Behavioral:**
- Double space in running text
- Text rendering twice (duplicated content block)
- Image area blank — asset not connected
- Wrong image vs. Figma spec
- Images cut off or cropped on mobile in a carousel
- Link has no underline and is not clickable
- Link leads to a 404 — launch blocker
- Last card in a horizontal scroll is half-cut

**Text on images (ALL folds):**
- Typo in a label inside a feature fold's UI/calendar screenshot (e.g., "participents")
- Participant/attendee names misspelled on a calendar or booking image
- Hover state on an image card has a typo
- Placeholder text inside a mockup never replaced

**Alt text:**
- Alt text is copy — compare every image alt against the content doc
- Items further in a carousel may have missing or wrong alt text
- Alt text typos are content issues — log in the issues table

**Inline anchor links:**
- A word the content doc specifies as hyperlinked exists on the page but is not clickable
- The wrong word in a sentence is linked instead of the specified word

**Sub line count:**
- One card sub wraps to 3 lines while all others are 2 — signals copy too long or spacing issue

**Analytics:**
- Two CTAs on the same fold with identical event names
- A search CTA missing an analytics event entirely

---

*Catch it now. Not after launch.*
