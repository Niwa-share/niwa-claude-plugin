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

## Before writing code

If the project's folder has a `NIWA.md`, read it first: it says which Niwa project this is and how the app is built.

Before writing code for something the person may put online, call `how_to_build_on_niwa` (start with the `overview` topic). Build only what it needs: a page that saves nothing is a static site, with no server or database. Information other visitors see goes in Postgres through `DATABASE_URL`, which Niwa adds; files go in `DATA_DIR`. Don't build sign-in: Niwa decides who gets in.

## Publishing

Publish only when the person has asked for it.

**Use the project's id.** You have it when the person gives it to you, when a `NIWA.md` in the folder names it, or when the person created or chose the project earlier in the chat. Otherwise never guess: publishing to the wrong project replaces someone's live app. Call `list_projects`, then ask the person which project to publish to, naming the one that looks closest, or whether to start a new one (`create_project`, once).

Then call `publish` with the project's id:

- **Where you can run commands in the project's folder** (Claude Code, or Cowork working on the person's computer): `publish` returns a one-time upload link and a command. Run that command from the project's top folder. It waits until the app is live, so you don't need `publish_status` unless it says so.
- **In a chat without that**: send the files themselves in `publish`'s `files`, for example a complete `index.html` (up to 300 files and 8 MB in total). Then call `publish_status` every 30 to 60 seconds until it says live or failed.

The upload's reply has a checklist, and when you published from a folder, the app's `NIWA.md` and what to do with it: do that. Fix what you can in the code and publish again; ask the person for anything only they know. Once it's live, give the person the address and say who can open it.

## Ask first

Always ask the person before changing who can open a project, inviting or removing anyone, or restoring a version. Never upload `.env` files, and never ask for secret values (API keys, passwords): the person adds them in Niwa, on the project's Secrets page.
