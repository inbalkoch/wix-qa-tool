# /qa — Page QA Workflow

## Step 1: Setup Check

Check if a file named `.setup-complete` exists in this folder.

**If it does NOT exist**, tell the user:

"Before your first QA, I need to verify your tools are connected. One-time setup — about 5 minutes."

Then check each of the following in order. For each one not connected, guide the user through connecting it before moving on:

1. **Google Drive MCP** — needed to read the content doc
   - Test: try listing recent files via the Google Drive MCP tool
   - If not connected: guide to Claude Code Settings → Integrations → enable Google Drive

2. **Chrome/Browser MCP** — needed to browse the staging page and run checks
   - Test: navigate to https://www.wix.com via the browser tool
   - If not connected: guide to enable Claude in Chrome browser integration

3. **Figma MCP** — needed to access the design file
   - Test: call get_metadata with fileKey "test" — expect auth error, not connection error
   - If not connected: guide to connect the Figma integration

4. **Google Workspace MCP** — needed to create the QA Google Sheet and log feedback
   - Test A (read): try reading range `Sheet1!A1:F1` from Sheet ID `1637r1DgyHs_upfx91kqfGjMFDTs1rBJMibAdVJivjuo`
   - If read fails: guide to Claude Code Settings → Integrations → enable Google Workspace
   - Test B (write): append a test row with the value "setup-test" to `Sheet1!A:A`, then immediately delete it by clearing that cell. This confirms edit access to the Feedback Sheet.
   - If write fails: tell the user — "Your Google account is connected but doesn't have edit access to the Feedback Sheet. Ask your QA tool admin to add your email as an Editor. You can still run QA — feedback just won't be logged until access is granted." Then continue setup.

When all four are confirmed: create `.setup-complete` with today's date. Tell the user:

"Setup complete. You're ready to run QA."

**If `.setup-complete` exists**: skip setup entirely. Go straight to Step 2.

---

## Step 2: Run QA

Read `qa-skill.md`. Follow it exactly. Start by asking the PMM for the 7 required inputs.

---

## Step 3: Log Feedback (After Delivering QA Sheet)

After delivering the QA sheet, ask exactly this:

"One quick question before we close: anything in this QA that felt off, missed something, or could be clearer? (Optional)"

Wait for their response. If they decline, that's fine.

Then silently log all feedback (corrections from during the session + anything said just now) to the central sheet.

**Sheet ID:** `1637r1DgyHs_upfx91kqfGjMFDTs1rBJMibAdVJivjuo`

**Ensure headers exist** — read `Sheet1!A1:F1`. If empty, write:

| A | B | C | D | E | F |
|---|---|---|---|---|---|
| Date | PMM | Page URL | Type | Comment | Context |

**Append one row per feedback item:**

- **Date**: today (YYYY-MM-DD)
- **PMM**: PMM name from the 7 inputs
- **Page URL**: mockup URL from the 7 inputs
- **Type**: `correction` (caught during session) or `suggestion` (from closing question)
- **Comment**: the specific feedback, verbatim or close paraphrase
- **Context**: which step or fold it relates to, or leave blank

If writing fails for any reason: skip silently. Do not surface errors to the PMM.
