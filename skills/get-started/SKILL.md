---
name: get-started
description: Use when someone first connects Niwa, asks what Niwa can do, or wants to share, publish or put online something they made (a page, a prototype, a site, an app) and get a link for it.
---

# Getting started with Niwa

Niwa hosts the web apps and sites people make with AI at `<name>.niwa.app`, and lets each project's owner choose who can open it. Every project starts private.

Niwa's tools come from its connector. If they aren't available, tell the person to connect Niwa first (in Claude Code: open `/mcp` and sign in to `niwa`; in Claude chat or Cowork: connect it on this plugin's Connectors tab), then carry on.

## When someone connects Niwa for the first time

1. Call `whoami` and greet them by name.
2. Call `list_projects`. If they have projects, say which are live and who can open each. If they have none, say so.
3. Tell them what they can ask for, in plain words:
   - "Publish this to Niwa" or "give me a link I can share" (`create_project`, `publish`)
   - "Is my latest version live?" (`publish_status`, `get_logs`)
   - "Show my versions" and "bring back yesterday's" (`list_versions`, `restore_version`)
   - "Share it with sam@example.com" or "make it public" (`invite_person`, `set_access`)

## Publishing

Publish only when the person has asked for it. Reuse an existing project from `list_projects` when there is one; otherwise call `create_project` once. Then call `publish`:

- **Where you can run commands in the project's folder** (Claude Code, or Cowork working on the person's computer): `publish` returns a one-time upload link and a command. Run that command from the project's top folder.
- **In a chat without that**: send the files themselves in `publish`'s `files`, for example a complete `index.html`. This takes up to 300 files and 8 MB in total.

The upload's reply has a checklist. Fix what you can in the code and publish again; ask the person for anything only they know. Call `publish_status` every 30 to 60 seconds until it says live or failed, then give the person the address and say who can open it.

## Ask first

Always ask the person before changing who can open a project, inviting or removing anyone, or restoring a version. Never upload `.env` files, and never ask for secret values (API keys, passwords): the person adds them in Niwa, on the project's Secrets page.
