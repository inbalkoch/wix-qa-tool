# Wix Page QA Tool

## Step 1 — Fetch Latest Version (Every Session)

Before doing anything else, fetch the latest QA process from the team source:

```bash
curl -fsSL "https://raw.githubusercontent.com/inbalkoch/wix-qa-tool/main/qa-skill.md" -o qa-skill.md \
  && echo "QA skill updated to latest version." \
  || echo "WARNING: Could not reach update server. Using local version — may not be current."
```

Then read `qa-skill.md`. That file defines everything you do. Do not proceed without reading it.

---

## Step 2 — Setup Check (First Time Only)

Check if a file named `.setup-complete` exists in this folder.

**If it does NOT exist**, run setup before anything else:

Tell the user: "Before your first QA, I need to verify your tools are connected. This is a one-time setup — takes about 5 minutes."

Check each of the following in order. For each one that is not connected, guide the user through connecting it step by step before moving to the next:

1. **Google Drive MCP** — needed to read the content doc (Google Doc)
   - Test: try listing recent files via the Google Drive MCP tool
   - If not connected: guide the user to enable it in Claude Code settings under Integrations

2. **Chrome/Browser MCP** — needed to browse the staging page and run checks
   - Test: try navigating to https://www.wix.com via the browser tool
   - If not connected: guide the user to enable Claude in Chrome or the browser integration

3. **Figma MCP** — needed to access the design file
   - Test: call get_metadata with fileKey "test" — expect an auth error, not a connection error
   - If not connected: guide the user to connect the Figma integration

When all three are confirmed working, create a file `.setup-complete` containing today's date. Tell the user: "Setup complete. You're ready to run QA."

**If `.setup-complete` exists**, skip to Step 3.

---

## Step 3 — Run QA

Follow `qa-skill.md` exactly. Start by asking for the 7 required inputs.

---

## Language

Always respond in English only.
