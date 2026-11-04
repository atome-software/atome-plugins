# Atome for Claude

Build and run your Atome app in your own words: add a field, a kanban view,
a page for the team, a form, an automation, or import your data, just by
saying it to Claude. The plugin connects Claude to Atome's own server and
brings the method that makes those changes safe: read first, show the plan,
ask before writing, read it back after.

*En français plus bas.*

## What is inside

- **Atome's connector**: Atome's remote MCP server, `https://api.atome.sh/mcp`, declared in
  `.mcp.json`. You sign in with your Atome account; Claude keeps the
  connection. There is no API key to paste.
- **Six skills**, plain text that Claude reads when a request matches:
  - `atome-interface`: fields, collections, views, pages, forms, access;
  - `atome-automation`: workflows and agents;
  - `atome-migration`: imports from another tool or a CSV file;
  - `atome-accueil`: getting to know your company, and keeping Atome's
    context up to date;
  - `atome-construire`: what Atome can do, and the rules to read before a
    change;
  - `atome-retour`: telling Atome's team what did not work, in at most
    three short reports that Claude shows you and sends only on your yes.

The same folder is ready as a plugin for Cursor and the other clients that
read the open [Agent Plugins](https://agent-plugins.org) format:
`plugin.json` and `mcp.json`, next to Claude's `.claude-plugin/plugin.json`
and `.mcp.json`, with the same six skills. It works in Cursor once Atome
accepts Cursor's sign-in.

Nothing runs on your computer: no hooks, no scripts, no executables, no
keys, no downloads. The plugin itself stores nothing; what Claude reads or
writes in your app goes only through Atome's connector, and a file you
share for an import is read in the conversation.

## Install

In Claude (web or desktop): **Customize > Plugins > Add > Add marketplace**,
enter `atome-software/atome-plugins`, choose **Atome**, then **Add**. Open the plugin's
**Connectors** tab (or **Customize > Connectors**), add **Atome** and
**Connect**: Atome's sign-in page opens. Your browser must be signed in to
the same Claude account as the app, or the connection won't hold. On a Team
or Enterprise plan, an Owner may need to allow the marketplace and add the
connector for the organisation.

The marketplace repository is public: no GitHub account and no Claude
GitHub App are needed (only private repositories need them). If the dialog
asks you to install the Claude GitHub App, skip it and use the Claude Code
commands below, typed in a session of the desktop app's Code tab.

In Claude Code:

```
/plugin marketplace add atome-software/atome-plugins
/plugin install atome@atome
/mcp
```

then choose `atome` and **Authenticate**. To get new versions on their own:
`/plugin`, **Marketplaces**, `atome`, **Enable auto-update**.

In Cursor: Atome doesn't accept Cursor's sign-in yet. Support is coming,
and this folder is ready for it.

## Signing in and what Claude can do

Atome's consent page asks which workspace Claude may use and what access it
gets. Reading is enough to explore your app; building needs write access to
records, and to pages and automations. Claude asks before every change and
never deletes a collection or a field, merges records or regenerates a
public link: those stay your clicks in Atome.

## Data and privacy

Claude calls Atome's tools under the access you granted; your data stays
between Claude and Atome. A report to Atome's team (`report_issue`) leaves
only on your yes, and carries the shape of a problem, never your names,
values or record contents. Atome's privacy policy: https://atome.sh/privacy.
Terms of use: https://atome.sh/terms.

## Support

https://atome.sh/support, or write to support@atome.sh.

## License

Apache License 2.0 (see `LICENSE`).

---

# Atome pour Claude

Construisez et faites tourner votre app Atome avec vos mots : un champ, une
vue kanban, une page pour l'équipe, un formulaire, une automatisation,
l'import de vos données, simplement en le disant à Claude. Le plugin relie
Claude au serveur d'Atome et apporte la méthode qui rend ces changements
sûrs : lire d'abord, montrer le plan, demander avant d'écrire, relire après.

Dedans : le connecteur d'Atome (son serveur MCP, `https://api.atome.sh/mcp`, avec « Se
connecter avec Atome », sans clé à coller) et six skills, du texte que
Claude lit quand une demande s'y rapporte. Rien ne tourne sur votre
ordinateur : ni crochet, ni script, ni exécutable, ni clé.

Pour l'installer dans Claude : **Personnaliser > Plugins > Ajouter > Ajouter
une marketplace**, `atome-software/atome-plugins`, **Atome**, **Ajouter** ; puis l'onglet
**Connecteurs** du plugin (ou **Personnaliser > Connecteurs**), **Atome**,
**Se connecter**, le navigateur connecté au même compte Claude que l'app. Le
dépôt est public : ni compte GitHub ni app GitHub de Claude (seul un dépôt
privé les demande). Si Claude propose d'installer l'app GitHub de Claude,
passez et tapez plutôt les lignes de Claude Code dans une session de
l'onglet Code de l'app. Dans Claude Code : `/plugin marketplace add
atome-software/atome-plugins`, `/plugin install atome@atome`, puis `/mcp`,
`atome`, **Authenticate**. Pour Cursor, ce dossier est prêt au format ouvert
Agent Plugins (`plugin.json`, `mcp.json`) : il y marchera dès qu'Atome
acceptera la connexion de Cursor.

Confidentialité : https://atome.sh/privacy. Conditions : https://atome.sh/terms.
Support : https://atome.sh/support, support@atome.sh.
