# Wix Page QA Tool

Automated page QA for PMMs. Runs in Claude Code.

## For PMMs: Getting Started

1. Install Claude Code: https://claude.ai/download
2. Download this folder (or clone this repo)
3. Open Claude Code from this folder
4. Type `/qa` — Claude will guide you through the one-time MCP setup, then you're ready

Setup takes about 10 minutes the first time. After that, open the folder and go.

---

## How Updates Work

This repo is maintained by the PMM team. When the QA process is updated, the change is pushed here.

Every time you start a QA session, Claude automatically fetches the latest `qa-skill.md` from this repo before doing anything. You always have the current version — no action needed on your side.

---

## For the Maintainer: Publishing Updates

When you update the QA skill in your system and want to push it to all PMMs:

1. Copy your updated `qa-skill.md` into this repo folder
2. Run: `git add qa-skill.md && git commit -m "update QA skill" && git push`
3. Done. Every PMM gets the update on their next session.

You never need to notify anyone or ask them to update. It's automatic.
