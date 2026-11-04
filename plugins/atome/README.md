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
- **Five skills**, plain text that Claude reads when a request matches:
  - `atome-interface`: fields, collections, views, pages, forms, access;
  - `atome-automation`: workflows and agents;
  - `atome-migration`: imports from another tool or a CSV file;
  - `atome-accueil`: getting to know your company, and keeping Atome's
    context up to date;
  - `atome-construire`: what Atome can do, and the rules to read before a
    change.

Nothing runs on your computer: no hooks, no scripts, no executables, no
keys, no downloads. The plugin itself stores nothing; what Claude reads or
writes in your app goes only through Atome's connector, and a file you
share for an import is read in the conversation.

## Install

In Claude (web or desktop): **Customize > Plugins > Add > Add marketplace**,
enter `atome-software/atome-plugins`, choose **Atome**, then **Add**. Open the plugin's
**Connectors** tab, add **Atome** and **Connect**: Atome's sign-in page
opens. On a Team or Enterprise plan, an Owner may need to allow the
marketplace and add the connector for the organisation.

In Claude Code:

```
/plugin marketplace add atome-software/atome-plugins
/plugin install atome@atome
/mcp
```

then choose `atome` and **Authenticate**. To get new versions on their own:
`/plugin`, **Marketplaces**, `atome`, **Enable auto-update**.

## Signing in and what Claude can do

Atome's consent page asks which workspace Claude may use and what access it
gets. Reading is enough to explore your app; building needs write access to
records, and to pages and automations. Claude asks before every change and
never deletes a collection or a field, merges records or regenerates a
public link: those stay your clicks in Atome.

## Data and privacy

Claude calls Atome's tools under the access you granted; your data stays
between Claude and Atome. Atome's privacy policy: https://atome.sh/privacy.
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
connecter avec Atome », sans clé à coller) et cinq skills, du texte que
Claude lit quand une demande s'y rapporte. Rien ne tourne sur votre
ordinateur : ni crochet, ni script, ni exécutable, ni clé.

Pour l'installer dans Claude : **Personnaliser > Plugins > Ajouter >
Ajouter une marketplace**, `atome-software/atome-plugins`, **Atome**, **Ajouter** ; puis
l'onglet **Connecteurs** du plugin, **Atome**, **Se connecter**. Dans Claude
Code : `/plugin marketplace add atome-software/atome-plugins`, `/plugin install
atome@atome`, puis `/mcp`, `atome`, **Authenticate**.

Confidentialité : https://atome.sh/privacy. Conditions : https://atome.sh/terms.
Support : https://atome.sh/support, support@atome.sh.
