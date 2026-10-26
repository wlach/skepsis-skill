---
name: skepsis
description: Run Oxide Skepsis for human review, then address or respond to inline feedback when the user finishes. Use when the user requests a Skepsis review.
---

# Skepsis review

Choose the user's requested mode (default: **respond**). Apply it after they finish reviewing:

- **address:** Make the requested changes, remove resolved review blocks, run appropriate checks, and summarize the result.
- **respond:** Consider each comment and explain your assessment and proposed changes in the conversation. Leave code and review blocks unchanged.

## Launch and hand off

- In the current worktree, run `skepsis` (or `npx --yes @oxide/skepsis`, requiring Node.js 22+). Use the requested diff scope; otherwise use the default. For working-copy-only review, use `--git -r HEAD` (Git) or `-r @` (jj). Inline comments require a diff ending at the working copy.
- Note existing `<review>...</review>` comments. Keep Skepsis running across turns and retain its process handle and worktree path.
- Verify startup, share the printed localhost URL, and say: **“Review in Skepsis and leave comments inline. Reply ‘done’ here when you're finished.”** End the turn. Leave reviewed files untouched while waiting.

## When the user finishes

- Skepsis writes `<review>...</review>` comments directly into source files. Read the current files and diff, including untracked files in scope, and handle new feedback in the selected mode. Include file locations in your response.
- Stop only the Skepsis process you started, unless the user wants it left open.

The user's reply is the completion signal.
