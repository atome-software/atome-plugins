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
enter `atome-software/atome-plugins`, then add **Atome**.

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
