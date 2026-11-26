# Alpine Reach plugin

Marketing answers for your AI agent, from your [Alpine Reach](https://www.alpinereach.io) workspace.

Ask your agent what ad to make for a product and it reads what the advertisers you track keep running on Meta: formats, opening lines, where the ads send people, how long each ad has run and which launch tests survived. It also works with your Alpine Reach content: brand context, drafts, calendar, analytics of your own accounts, strategy and media.

## What is inside

- **MCP server** `https://app.alpinereach.io/api/mcp`, signed in with your Alpine Reach account. You approve which workspaces and what access the agent gets inside Alpine Reach. Tools update the moment Alpine Reach ships; nothing to reinstall.
- **Skills** that teach the agent how to use the tools:
  - `alpine-reach-setup`: connect, approve and choose the project.
  - `ad-research`: turn competitors' long running Meta ads into a recipe for your next ads.

The answer tools read data your workspace already stores. They never start a paid read.

## Install

Claude Code:

```
/plugin marketplace add Girolino/alpine-reach-plugin
/plugin install alpine-reach@alpine-reach
```

Then run `/mcp`, choose `alpine-reach` and sign in with your Alpine Reach account. To get updates automatically, turn on auto-update for the `alpine-reach` marketplace in `/plugin`.

Claude (web, desktop) and Cowork: add the plugin from the directory once it is listed, then connect Alpine Reach from the plugin's Connectors tab.

## Your data

Alpine Reach returns only data from projects you approved, under your current role in each workspace. Disconnect at any time in Alpine Reach, Settings, AI assistants.

## Support

Open an issue in this repository, or write from Alpine Reach, Settings.

## License

MIT
