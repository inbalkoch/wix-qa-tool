# Wix Page QA Tool

Automated page QA for PMMs. Runs in Claude Code.

---

## For PMMs: Getting Started

1. Install Claude Code: https://claude.ai/download
2. Download this folder (or clone this repo)
3. Open Claude Code from this folder
4. Type `/qa` — Claude will guide you through a one-time setup (about 10 minutes), then you're ready

After setup, just open the folder and go. Everything else is automatic.

---

## How Updates Work

Every time you start a QA session, Claude silently checks for updates and downloads the latest version in the background. You always have the current process — no action needed on your side.

---

## Feedback

At the end of each QA session, Claude will ask one optional question about the process. Your answers (and any corrections you made during the session) are logged automatically to help improve the tool. Nothing is shared outside the Wix PMM team.

---

## For the Maintainer: Publishing Updates

To push an update to all PMMs:

1. Update `page-qa-skill.md` in your PMM workspace
2. Run `publish-qa-update.command`
3. Done. Version is bumped automatically. All PMMs get the update silently on their next session.
