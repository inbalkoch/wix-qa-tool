---
name: page-qa-skill
description: QA a built web page against the content doc and visual/behavioral standards. Use when a PMM needs to review a page before launch — covers content accuracy, typos, SEO metadata, visual bugs, mobile, and produces a structured QA sheet.
---

# Page QA Skill

Check the page. Catch what's broken. Give the PMM a clear, actionable QA sheet.

## When to Use

- A PMM says they want to QA a page
- A page has been built and needs review before launch
- Content, design, or visual issues need to be documented
- A structured QA sheet needs to be produced for the team

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

A page QA has three layers:

| Layer | What You're Checking |
|-------|---------------------|
| **Content** | Does every word on the page match the content doc exactly? Any typos? Does SEO metadata match? |
| **Design** | Does the page look like the Figma file (layout, typography, colors, images)? |
| **Visual / Behavior** | Are there bugs, broken elements, or behavioral issues? |

Each issue found becomes one row in the QA sheet.

**The content doc is the sole authority for all copy.** The Figma file is used for design and layout checks only — never for verifying text. If the Figma shows different copy than the content doc, the content doc wins.

---

## Step-by-Step QA Process

### Step 1: Content Check (Page vs. Content Doc)

Open the content doc and the live page side by side.

Go section by section, top to bottom:

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
- [ ] **Alt text matches content doc** — for every image that has a specified alt text in the content doc, confirm it matches exactly. Run the alt text check in Step 3b to pull all image alts at once. Log mismatches as content issues.
- [ ] Send-off / closing line is complete and punctuated correctly
- [ ] **SEO Title:** Confirm the page title matches what the content doc specifies
- [ ] **SEO Meta Description:** Confirm the meta description matches the content doc exactly (check in page source or browser dev tools)

**The content doc is the sole authority.** Do not use Figma copy as a reference when checking content.

**Log every discrepancy as an issue. Even one wrong word, missing period, or typo is an issue.**

---

### Step 2: Design Check (Page vs. Figma)

Design check covers visual layout, typography style, colors, images, and spacing ONLY. Do not use Figma to verify copy — the content doc is the sole authority for all text.

**How to access Figma — try in this order:**

**Option 1: Figma MCP tools (try first)**
Do not open the Figma URL as a browser link. Parse the URL instead:
- From `https://figma.com/design/AbCdEfG/FileName?node-id=1-2`
- `fileKey` = `AbCdEfG`
- `nodeId` = `1:2` (replace `-` with `:`)

1. Run `get_metadata` to get the file structure and identify all frames/sections
2. For each section/fold, run `get_design_context` to get a screenshot and design details
3. Compare each Figma frame against the corresponding section on the live page

**Option 2: PNG export (fallback if Figma MCP is unavailable or browser navigation to figma.com is blocked)**
Ask the PMM: "The Figma file is not accessible from my session. Please export the final approved frames as PNG — one image per fold/section — from Figma (File > Export) and share them here."
Once the PMM shares the PNGs, compare each image fold by fold against the live page using the same checklist below.

**Never skip the design check.** If Figma is inaccessible and the PMM has not yet shared PNGs, pause and ask before continuing.

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
- [ ] **Sub line count consistency:** Check the number of lines each sub/body text occupies within a fold. If all card subs in a fold are 2 lines and one card goes to 3 lines, flag it — this signals either copy is too long or a line-break/spacing issue. Compare against other cards in the same fold as the baseline.

**Images & Media:**
- [ ] Correct image is used (not a placeholder)
- [ ] Image matches the Figma — if a different image appears on the page than what the Figma specifies, flag it as a wrong asset
- [ ] Image aspect ratio matches Figma
- [ ] Image is not pixelated or blurry
- [ ] Videos/animations are present and playing
- [ ] Images in carousels or scrollable sections are not cut off or cropped on either desktop or mobile. Scroll through the full carousel to verify all items are fully visible.
- [ ] **Text on images (ALL folds, not just template cards):** Read all text that appears inside or overlaid on any image across the entire page — UI screenshots, product mockups, calendar previews, app screens, feature fold illustrations, labels on graphics, event/booking examples in calendar images. Check for typos, wrong words, and copy mismatches. Do not limit this check to template cards or the template section. Apply it to every fold that contains an image with visible text inside it.
- [ ] **Alt text completeness — scrollable/carousel sections:** For every scrollable or carousel section, scroll through ALL items (not just the ones visible on load) and confirm each image has accurate alt text. Flag images with missing alt text or alt text that contains typos.

**Colors & Styles:**
- [ ] Background colors match
- [ ] Button colors and styles match
- [ ] Icon colors match
- [ ] Border radius, shadows match

**CTAs & Buttons:**
- [ ] Button style matches Figma
- [ ] Button position matches
- [ ] Hover state looks correct (if visible)
- [ ] **Hero CTA is visible above the fold WITHOUT scrolling** — on both desktop and mobile. If the CTA requires scrolling to see it on either view, flag as an issue.
- [ ] **Each fold has a visible CTA button** — confirm the "Get Started" (or equivalent) button is present and visible on every fold that should have one per the Figma spec. Flag any fold where the CTA is missing or hidden.

---

### Step 3: Visual & Behavioral Issues

Look for bugs that don't fit neatly into content or design. Check these specifically:

**Text Issues:**
- [ ] Double spaces between words
- [ ] Widows (single word on last line) in important headlines
- [ ] Text that is cut off or overflowing its container
- [ ] Text that is too small to read at normal zoom
- [ ] Text rendering twice (duplicated content blocks)

**Link Issues:**
- [ ] Links that look like links but are not clickable
- [ ] Underlined text that is NOT a link
- [ ] Links opening in wrong tab (internal links should stay in same tab, external can open new)
- [ ] **404 check:** Click every visible link and CTA on the page. If any link leads to a 404 or error page, flag it as an issue with the exact link text and location. A broken link is a launch blocker.
- [ ] **Destination check:** For every link that has a specified URL in the content doc, click it and confirm the page it lands on matches. If the link goes to a different URL than what the content doc specifies, flag it as an issue. Write the expected URL (from content doc) and the actual URL (where it went) in the How to Fix column. If the content doc does not specify a URL for a link, flag it for PMM manual verification.
- [ ] **Inline anchor check:** When the content doc specifies that a particular word or phrase should be hyperlinked (e.g., "site plan" links to wix.com/plans), verify that the exact word/phrase on the page is actually clickable — not just that the URL is reachable. Flag if the word exists on the page but is not hyperlinked, or if a different nearby word is linked instead.

**Images:**
- [ ] Images that look pixelated or stretched
- [ ] Images that fail to load (broken img placeholder)
- [ ] Alt text missing on important images (accessibility)

**Scroll & Overflow:**
- [ ] No horizontal scroll on desktop (unless intentional carousel)
- [ ] Horizontal scrollable sections let the user reach the last item (not stuck)
- [ ] Page scrolls smoothly, no janky jumps
- [ ] Sticky headers not blocking content

**Interactive Folds (Accordions, Tabs, Carousels, etc.):**
- These are hard to fully verify visually. For each interactive element:
  - Note which fold it is and what type of interaction it uses
  - Add a flag for the PMM to manually test the behavior

---

### Step 3b: SEO Technical Checks

Run these via `javascript_tool` in the browser. They do not require view-source or DevTools access — all are readable from the live DOM.

**How to run each check:**

- **OG tags:** `[...document.querySelectorAll('meta[property^="og:"]')].map(m => m.getAttribute('property') + ': ' + m.getAttribute('content'))` — confirm `og:title`, `og:description`, `og:image`, `og:image:width`, `og:image:height`, and `og:site_name` are all present. Flag any that are missing.
- **Schema markup:** `[...document.querySelectorAll('script[type="application/ld+json"]')].map(s => s.textContent)` — confirm at least one schema block is present. Log the type and flag for SEO Manager to confirm the correct schema is used.
- **External link rel attributes:** `[...document.querySelectorAll('a[href]')].filter(a => a.hostname !== location.hostname && a.rel).map(a => a.href + ' → rel=' + a.rel)` — if the SEO spec requires link equity to pass, flag any external links that include `noopener` or `noreferrer`.
- **Image filenames:** `[...document.querySelectorAll('img')].map(i => i.src.split('/').pop())` — review filenames for SEO-meaningful naming. Flag generic filenames (e.g., `image1.jpg`, `unnamed.png`) if the SEO spec requires descriptive filenames.
- **Hero image format/optimization:** Read the hero image `src` — flag if the extension is `.jpg` or `.png` instead of `.webp` or `.avif`. For size, use `fetch(src, {method:'HEAD'})` to get the `content-length` header and flag if over 200KB.
- [ ] **Alt text — presence and accuracy:** Run `[...document.querySelectorAll('img')].map(i => ({src: i.src.split('/').pop(), alt: i.alt}))` to get all image alt texts. Then compare each alt text against the content doc: (1) flag any image with missing alt text, (2) flag any alt text that does not match the content doc exactly (wrong words, typos, truncated). Alt text is copy — the content doc is the sole authority. For carousel/scrollable sections, scroll to load all items before running the check.

---

### Step 4: Mobile Check

Repeat steps 1–3 on mobile view (320px–375px width).

Mobile-specific checks:

- [ ] Text is readable without pinching
- [ ] Buttons are large enough to tap (min 44px)
- [ ] Nothing is cut off on the right edge
- [ ] Images stack correctly (not side by side when too small)
- [ ] Images in carousels or scrollable sections (e.g., template cards) are not cut off or cropped — scroll through the full section on mobile to verify all items are fully visible
- [ ] Navigation/hamburger menu works (note for PMM to test)
- [ ] CTAs are visible above the fold on mobile
- [ ] No horizontal scroll on mobile
- [ ] Spacing feels proportional (not too tight, not too loose)
- [ ] Interactive elements are noted for PMM to manually test on device

---

### Step 5: What the PMM Must Check Manually

Some things cannot be verified without a real device or account. Always include this section in your output.

Keep the manual checks table concise — group by category.

**Note on links:** Link destinations that are specified in the content doc are verified in Step 3 (Destination check). Only links with NO specified URL in the content doc go in the manual checks table.

**The PMM needs to manually verify:**
1. Links where the content doc does not specify a destination URL — PMM to confirm they go to the correct place
2. All interactive element behaviors (accordions, carousels, search forms, template cards) — behavior cannot be verified remotely
3. Mobile behavior on a real device
4. Analytics / event tracking: for each CTA and interactive element, confirm (a) the click event fires, (b) each event has a unique, distinct name (two CTAs on the same fold must not share the same event name), and (c) no CTA is missing an event entirely. Flag any CTA that does not have a specified event name in the analytics spec.
5. SEO meta description in page head (exact match to content doc)
6. Schema markup correctness — SEO Manager to confirm the schema type found in Step 3b is the correct type for this page

---

## Output: The QA Sheet

**Every QA session must produce TWO outputs — both are required:**

1. **Markdown file** — saved to `O-output/[page-name]-qa/qa-sheet.md`. Contains the full report: header, issues table, manual checks table, and the Google Sheet link in the header.
2. **Google Sheet** — created from the same content and link shared directly in the chat. The sheet must contain all three sections in one sheet: header, issues table, manual checks table.

Neither output is optional. Do not deliver one without the other.

Produce the QA output in this exact format. Each issue is one row.

### QA Sheet Header

```
PAGE QA REPORT
==============
Mockup URL:      [staging/preview URL]
Page URL:        [final URL from content doc]
QA Date:         [today's date]

Google Sheet:    [link to the Google Sheet — add this after the sheet is created]

Team:
  PMM:           [name]
  SEO Manager:   [name]
  Content:       [name]
  Design:        [name]
  Tech Design:   [name]
```

**Note:** The Google Sheet link goes in the header of the md file as well. Create the sheet first (see Google Sheet Delivery section below), then add the link to the md header before saving.

### Issues Table

One row per issue. Use this column structure:

| # | Issue Type | Requested By | Desktop / Mobile | Issue | How to Fix | Screenshot | Fixed by tech design | Approved | Comments |
|---|---|---|---|---|---|---|---|---|---|

**Field instructions:**
- **#** — Sequential issue number
- **Issue Type** — Category label. Choose one: `Content`, `Design`, `SEO`, `Technical`, `Accessibility`. In the Google Sheet, the cell background color reflects the type (see Issue Type Reference below). When in doubt: if it's about text or copy, it's Content; if it's about how something looks vs Figma, it's Design; if it's about search visibility, it's SEO; if it's about something broken or not working, it's Technical; if it's about missing alt text or visibility, it's Accessibility.
- **Requested By** — PMM name (same for all rows)
- **Desktop / Mobile** — "both", "Desktop", or "Mobile"
- **Issue** — SHORT. Just the location and problem name. Example: "Fold 8, loyalty program sub — wrong wording." Not a full paragraph.
- **How to Fix** — The full detail. Include exact replacement copy where relevant, formatted clearly. This is where the length lives, not in the Issue column.
- **Screenshot** — Note "Snagit recommended" or leave blank
- **Fixed by tech design** — Leave empty (team fills this in)
- **Approved** — Leave empty (team fills this in)
- **Comments** — Leave empty (team fills this in)

**Issue writing style:**
```
Bad:  "Fold 8 (Revenue): 'Loyalty program' sub has wrong wording. Page says 'points for every booking they make on your scheduling system.' Content doc says 'points for every booking made on your scheduling system.'"
Good: "Fold 8, loyalty program sub — wrong wording."

The fix column then reads: "Change 'they make on' to 'made on'."
```

Closely related issues in the same fold (e.g., two cards both have wrong subs) can be grouped in one row when the fix instructions are clear for each item.

### Manual Checks Table

After the issues table, add a short manual checks section. Keep it concise — group by category, do not list every individual link.

```
MANUAL CHECKS FOR PMM
======================
These items cannot be verified remotely and require manual testing:

| # | What to Check |
|---|---------------|
```

Use this template:

| # | What to Check |
|---|---------------|
| 1 | CTAs: Confirm all "Get Started" buttons link to the correct destination. Confirm click events fire. |
| 2 | Links: Confirm all inline and text links navigate to the correct URLs. |
| 3 | Interactive elements: Test [list the specific interactive elements found on this page, e.g., FAQ accordion, domain search form, template cards]. |
| 4 | Mobile: Test hamburger menu and all interactive elements on a real device. |
| 5 | Analytics: Confirm all click events fire correctly (GA4/BI per spec). Each CTA must have a unique event name — verify no two CTAs on the same fold share the same event name, and no CTA is missing an event entirely. |
| 6 | SEO: Confirm meta description in page head matches content doc exactly. |
| 7 | SEO (Schema): Confirm the schema type found in the automated check is the correct type for this page. |

### Issue Type Reference

Use this table to assign the correct type to each issue. Each type has a dedicated color applied to its cell in the Google Sheet.

| Type | Cell Color | What Qualifies |
|------|-----------|----------------|
| **Content** | Light blue `#D6EAF8` | Wrong copy, typos, missing/extra text, wrong alt text, punctuation issues, CTA wording mismatch, capitalization, send-off errors |
| **Design** | Light purple `#E8DAEF` | Figma mismatch (font, color, spacing, layout, images), wrong asset used, wrong image aspect ratio, pixel/blur issues, button style deviation, sub line count inconsistency |
| **SEO** | Light green `#D5F5E3` | Missing/wrong meta title or description, OG tags, schema markup, image filenames not descriptive, hero image format or size, structured data |
| **Technical** | Light orange `#FDEBD0` | Broken links (404s), broken images, double spaces, text rendering twice, wrong link destination, inline anchor not linked, carousel item cut off, horizontal scroll, interactive element bugs |
| **Accessibility** | Light yellow `#FEF9E7` | Missing alt text, tap targets too small, text cut off or overflowing container, text too small to read, CTAs not visible above the fold |

**Mobile is not a type.** Mobile issues are typed as Content, Design, Technical, etc. The type tells you *what kind of problem it is*; the Desktop/Mobile column tells you *where it appears*.

---

### Google Sheet Delivery (MANDATORY)

After saving the QA sheet as a markdown file, create a Google Sheet with the same content and share the link directly in the chat.

**The Google Sheet must include all three sections in a single sheet:**
1. Page header (PAGE QA REPORT label, Mockup URL, Page URL, QA Date, Google Sheet link, team names)
2. Issues table (all rows, with all 9 columns)
3. Manual checks table (all rows)

**How to create it:**
1. Write a CSV file to `/tmp/qa-sheet-full.csv` using Python's `csv` module with `quoting=csv.QUOTE_ALL` to handle commas and special characters in the content
2. Base64 encode it with `base64 -i /tmp/qa-sheet-full.csv` (macOS syntax — the `-i` flag is required)
3. Upload via the Google Drive MCP `create_file` tool with `mimeType: text/csv` — Google Drive auto-converts it to a Google Sheet
4. **Apply Issue Type colors:** After the sheet is created, use the Google Workspace MCP `sheets-batch-update` tool to apply background colors to the Issue Type column (column B in the issues table). For each row, apply the color that matches its Issue Type value:
   - `Content` → `#D6EAF8`
   - `Design` → `#E8DAEF`
   - `SEO` → `#D5F5E3`
   - `Technical` → `#FDEBD0`
   - `Accessibility` → `#FEF9E7`
   Use `userEnteredFormat.backgroundColor` in the `repeatCell` request. Target only the Issue Type cells in the issues table rows — not the header row or the manual checks section.
5. Share the resulting link in the chat — as a plain, clickable URL. No exceptions. This exact format:

```
QA sheet delivered. Here is your Google Sheet with all issues and manual checks:

https://docs.google.com/spreadsheets/d/[FILE_ID]/edit
```

The link must appear as a plain URL in the chat, not embedded in markdown text. Do not describe it without showing it.

**Never skip this step.** The Google Sheet is the primary deliverable the PMM shares with the team. The markdown file is the local backup.

---

## QA Rules

### Rule 1: One Issue Per Row (with exceptions)
Each distinct issue gets its own row. Closely related issues in the same fold (e.g., two cards with wrong subs, two H3 titles both wrong) can be grouped in one row when the fix instructions cover each item clearly.

### Rule 2: Short Issue, Detailed Fix
The Issue column should be short — location and problem name only. The How to Fix column is where the detail goes, including exact replacement copy.

```
Issue column:   "Fold 10, Card 2 — H3 title wrong."
How to Fix:     "Replace with: 'Web hosting and domains.'"
```

### Rule 3: Desktop and Mobile
If an issue appears on both, note "both" in the Desktop/Mobile column. Only split into separate rows if the issue manifests differently on each.

### Rule 4: Never Skip a Section
Even if a section looks perfect, mentally confirm it. Silent approval is still approval.

### Rule 5: Interactive Elements Are Always PMM's Job
Note them in the manual checks table. Do not try to verify behavior remotely.

### Rule 6: Content Doc Is the Authority
If the page copy differs from the content doc, it is an issue — regardless of what the Figma shows.

---

## Quality Checklist (Before Submitting QA)

- [ ] Collected all 7 inputs from PMM before starting?
- [ ] Checked every section of the page against the content doc?
- [ ] Checked for typos, spelling errors, and missing punctuation?
- [ ] Checked SEO title and meta description against content doc?
- [ ] Checked design against the Figma file?
- [ ] Checked all visual and behavioral issues?
- [ ] Clicked every link — checked for 404s?
- [ ] Checked link destinations against content doc URLs — mismatches logged as issues?
- [ ] Checked inline anchor links — specific words that should be hyperlinked actually are?
- [ ] Read text inside ALL images across ALL folds (not just template cards)?
- [ ] Scrolled through all carousel/scrollable sections and checked alt text on every item?
- [ ] Checked sub line count consistency within each fold?
- [ ] Ran Step 3b SEO checks via JavaScript: OG tags, schema, external link rel attributes, image filenames, hero image format/size?
- [ ] Checked mobile view?
- [ ] Manual checks table only contains links with no specified URL in the content doc?
- [ ] Analytics manual check specifies distinct event names per CTA, not just "confirm events fire"?
- [ ] Issue Type assigned to every row (Content / Design / SEO / Technical / Accessibility)?
- [ ] Issue column is short — location and problem name only?
- [ ] How to Fix column has all the detail, including exact replacement copy?
- [ ] Google Sheet created and link shared in chat?
- [ ] Google Sheet link added to the md file header?

---

## Common Issues to Watch For

**Content:**
- Hero headline doesn't match content doc (often updated in doc after build started)
- CTA button text differs from content doc by one word
- Missing legal text at the bottom of the page
- Send-off or tagline missing final period
- Typo on a CTA hover state or image overlay (easy to miss)

**Design:**
- Font weight is Regular instead of SemiBold
- Section background color is slightly off (e.g., #F7F7F7 vs. #F5F5F5)
- Mobile image is the desktop image squeezed (wrong asset used)

**Visual/Behavioral:**
- Double space in running text
- Text rendering twice (duplicated content block)
- Image area blank/white — asset not connected
- Wrong image on the page vs. Figma spec (different photo, different UI screenshot)
- Images cut off or cropped on mobile in a carousel or scrollable section
- "Learn more" link has no underline and is not clickable
- Link leads to a 404 — flag immediately with the exact location and link text
- Last card in a horizontal scroll is half-cut

**Text on images (common miss — applies to ALL folds, not just template cards):**
- Typo in a label or UI element visible inside a product screenshot in a feature fold (e.g., "participents" in a calendar preview image)
- Participant/attendee names misspelled on a calendar or booking image
- CTA hover state on an image card has a typo (e.g., "Lee Mor terapist" instead of "Lee Mor therapist")
- App screen or mockup shows placeholder text that was never replaced
- Text inside a feature fold's illustration or UI mockup is easy to miss — always zoom in and read it

**Alt text:**
- Alt text is copy — treat it the same as any other text on the page. The content doc specifies the correct alt text. Compare every image alt against the content doc.
- Items not visible on initial load (further in a carousel) may have missing or wrong alt text — scroll to the end to load all items before running the alt check
- Typos in alt text (e.g., "tatoos", "terapist") are content issues, not just accessibility issues — log them in the issues table

**Inline anchor links:**
- A word the content doc specifies should be hyperlinked (e.g., "site plan") exists on the page but is not actually clickable
- The wrong word in a sentence is linked instead of the specified word

**Sub line count:**
- One card sub in a fold wraps to 3 lines while all others are 2 lines — signals copy too long or spacing issue

**Analytics:**
- Two CTAs on the same fold with identical event names — must be distinct
- A search CTA (e.g., domain search) has no analytics event at all

---

## Integration with ABC-TOM

When using this skill:

1. **Ask PMM first** — Collect all 7 inputs before opening any link
2. **Check methodically** — Top to bottom, section by section, don't jump around
3. **Output to O-output** — Save the QA sheet in `O-output/[page-name]-qa/`
4. **Flag for Loop** — Note any patterns in how pages are commonly built wrong, update `M-memory/learning-log.md`

---

*Catch it now. Not after launch.*

---

> **© Tom Even**
> Workshops & future dates: [www.getagents.today](https://www.getagents.today)
> Newsletter: [www.agentsandme.com](https://www.agentsandme.com)
