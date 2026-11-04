<p align="center">
  <img src="plugins/atome/assets/icon.png" width="96" height="96" alt="Atome">
</p>

<h1 align="center">Atome for Claude</h1>

<p align="center">The official <a href="https://atome.sh">Atome</a> plugin for Claude: Atome's connector and the skills to build your Atome app in your own words.</p>

## Install

In Claude Code:

```
/plugin marketplace add atome-software/atome-plugins
/plugin install atome@atome
```

In Claude (web or desktop): **Customize > Plugins > Add > Add marketplace**,
enter `atome-software/atome-plugins`, then add **Atome**. Open the plugin's **Connectors** tab (or
**Customize > Connectors**) and connect Atome, with your browser signed in to
the same Claude account as the app. This repository is public: no GitHub account
and no Claude GitHub App are needed (only private repositories need them). If
the dialog asks you to install the Claude GitHub App, skip it and use the Claude
Code commands above, typed in a session of the desktop app's Code tab.

For Cursor, [`plugins/atome`](plugins/atome) is ready in the open
[Agent Plugins](https://agent-plugins.org) format: it works once Atome
accepts Cursor's sign-in.

## What it does

- Connects Claude to your Atome workspace: you sign in with your Atome account, no API key.
- Builds your app as you describe it: fields, views, pages, forms, automations, agents, each change shown before it is made.
- Imports your data from another tool or a CSV file.

## Connector

[https://api.atome.sh/mcp](https://api.atome.sh/mcp), Atome's remote MCP server. Nothing runs on your
computer: no hooks, no scripts, no keys. More in
[the plugin's README](plugins/atome/README.md).

## License

[Apache-2.0](LICENSE)
