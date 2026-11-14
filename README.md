# Niwa for Claude

Niwa puts the apps and sites you make with AI on the web, at `your-project.niwa.app`. Projects start private, and you choose who can open them. This plugin connects Claude to Niwa, so you can say "publish this to Niwa" or "give me a link I can share" and Claude does the rest.

## What you can ask for

- **Publish.** "Publish this to Niwa." Claude sends the project, fixes what it can, and asks you only for things only you know. A minute or two later it's live.
- **Check.** "Is my latest version live?" "Why did the last publish fail?" Claude reads the status and the build log.
- **Go back.** "Show my versions" and "bring back yesterday's." Every publish is kept as a version.
- **Share.** "Share it with sam@example.com" or "make it public." Claude asks you before it changes who can open a project.

## What's in the plugin

- A connector to Niwa's MCP server at `https://dashboard.niwa.app/mcp`. You sign in to Niwa once (OAuth) to allow it. There is no API key to paste.
- One skill, `get-started`, that tells Claude how to greet you, show your projects, and publish.

There are no hooks, scripts or local programs: nothing in this plugin runs on your computer.

## What it sends, and where

The plugin talks to one service, Niwa (`dashboard.niwa.app`), as the Niwa account you signed in with. When you ask Claude to publish, the project's files are uploaded to Niwa so it can host them. Claude is told never to upload `.env` files or other secrets. Nothing is sent anywhere else.

Niwa is a product of Mooji, Inc. See Niwa's [privacy policy](https://www.niwa.app/privacy) and [terms](https://www.niwa.app/terms).

## You need a Niwa account

Niwa is invite-only while we let people in a few at a time. [Ask for an invite](https://www.niwa.app/request) if you don't have an account yet.

## Install

On claude.ai or in the Claude desktop app, open **Customize > Plugins**, find Niwa, and add it. Then connect Niwa on the plugin's **Connectors** tab.

In Claude Code:

```sh
claude plugin marketplace add Niwa-share/plugin
claude plugin install niwa@niwa-app
```

Then open `/mcp` in a session and sign in to `niwa`.

## Help

[www.niwa.app/support](https://www.niwa.app/support) or support@niwa.app.

## License

MIT. Copyright (c) 2026 Mooji, Inc. See [LICENSE](./LICENSE).
