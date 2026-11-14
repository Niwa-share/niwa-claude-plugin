---
name: get-started
description: Use when someone first connects Niwa, asks what Niwa can do, or wants to share, publish or put online something they made (a page, a prototype, a site, an app) and get a link for it.
---

# Getting started with Niwa

Niwa hosts the web apps and sites people make with AI at `<name>.niwa.app`, and lets each project's owner choose who can open it. Every project starts private.

Niwa's tools come from its connector. If they aren't available, tell the person to connect Niwa first, then carry on:

- **Claude Code:** open `/mcp` and sign in to `niwa`.
- **Claude chat or Cowork:** connect Niwa on this plugin's Connectors tab.
- **Codex:** install the plugin again (`codex plugin install niwa@niwa-app`), which asks them to sign in to Niwa.
- **ChatGPT:** connect Niwa again where ChatGPT's settings list its plugins and apps.

## When someone connects Niwa for the first time

1. Call `whoami` and greet them by name.
2. Call `list_projects`. If they have projects, name each with its address and who can open it. It doesn't say whether each is running: call `get_project` for the ones they ask about. If they have none, say so.
3. Tell them what they can ask for, in plain words:
   - "Publish this to Niwa" or "give me a link I can share" (`create_project`, `publish`)
   - "Is my latest version live?" (`publish_status`, `get_logs`)
   - "Show my versions" and "bring back yesterday's" (`list_versions`, `restore_version`)
   - "Share it with sam@example.com" or "make it public" (`invite_person`, `set_access`)

## Building for Niwa

If the project's folder has a `NIWA.md`, read it first: it says which Niwa project this is and how the app is built.

Before writing code for something the person wants to put online with Niwa, call `how_to_build_on_niwa` (start with the `overview` topic). In short:

- Add only what it needs. A page that saves nothing is a static site: an `index.html`, no server or database.
- Information other visitors see goes in Postgres through `DATABASE_URL`, which Niwa adds. Not SQLite or JSON files.
- Files go in `DATA_DIR` (`/data`). Anything saved elsewhere on the server is wiped at each publish.
- A server app listens on `PORT` (8080).
- Don't build sign-in: Niwa decides who gets in, and tells the app who's visiting.

## Publishing

Publish only when the person has asked for it.

**Use the project's id.** You have it when the person gives it to you, when a `NIWA.md` in the folder names it, or when the person created or chose the project earlier in the chat. Otherwise never guess: publishing to the wrong project replaces someone's live app. Call `list_projects`, then ask the person which project to publish to, naming the one that looks closest, or whether to start a new one (`create_project`, once).

Then call `publish` with the project's id, and follow what its reply says:

- **Where you can run commands in the project's folder** (Claude Code, Codex, or Cowork working on the person's computer): `publish` returns a one-time upload link and commands. Run `command` from the project's top folder: it uploads the code with Niwa's small helper (`npx`) and waits until the app is live. If `npx` isn't there, run one of the other commands it gives; they only upload, so then follow the build with `publish_status`.
- **In a chat, or when commands can't reach the internet** (a sandbox without network access): call `publish` again with the project's files in `files`, for example a complete `index.html` (up to 300 files and 8 MB in total). Then follow the build with `publish_status`.

To follow a build, call `publish_status` every 30 to 60 seconds until it says live, failed or crashed. If it failed or crashed, read the log it gives, fix the code and publish again.

The reply after an upload has a checklist and, when you published from a folder, the app's `NIWA.md` and what to do with it: do what both say. Fix what you can in the code and publish again; ask the person for anything only they know.

Once it's live, tell the person. If the chat shows Niwa's card, the card already shows the address and who can open it: one short sentence is enough. Otherwise give them the address and say who can open it.

## When Niwa isn't the answer

Use Niwa's tools only for putting something the person made online with Niwa, and for their Niwa projects. Answer everything else (writing, questions, code that isn't going on Niwa) without them. If the person names another hosting service, like Netlify or Vercel, help them with that one; don't call Niwa's tools or steer them to Niwa.

## Ask first

Always ask the person before changing who can open a project, inviting or removing anyone, or restoring a version, even when they say not to ask. Ask about each project by name: never change several projects at once.

Never upload `.env` files or other secrets. Secret values (API keys, passwords) are added by the person on the project's Secrets page in Niwa: never ask for them, and never put them in code or in the chat.
