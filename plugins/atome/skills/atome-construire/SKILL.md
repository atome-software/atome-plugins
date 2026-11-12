---
name: atome-construire
description: Answer a question about what Atome can do and how, without changing anything, and give the rules to read before any change through Atome's connector. Fields and their 22 types, relations, lookups, rollups, formulas, views, pages, forms, workflows, agents, access, the company brain. « C'est quoi la différence entre un lookup et un rollup ? », « quels types de champs existent ? », « est-ce qu'une formule peut calculer une date ? », « peut-on filtrer une vue par l'utilisateur connecté ? », « un workflow peut-il envoyer un mail ? ». Use it for any question about Atome, and read it again before each change of an Atome app.
---

# What Atome can do, and how we know it

This skill answers questions about Atome and gives the rules to read before
changing an app. It writes nothing. Answer simply, in the person's language,
from your first message, with an example from their own app when it helps;
say when a rule is still an open question rather than asserting it. If the
question leads to a change, offer to make it (the atome-interface and
atome-automation skills).

## Where the truth is

1. **Their app, live.** `list_collections`, `describe_collection` (with
   `raw: true` for each field's stored shape), `list_pages` and
   `get_page_view`, `list_workflows` and `get_workflow`, `get_access_rules`,
   the brain (`list_brain_files`, `read_brain_file`). Read; never answer
   from memory about their app.
2. **Atome's published grammar**, at https://api.atome.sh/docs/atome-grammar: Markdown, no key, generated from
   Atome's own definitions for the build that runs. It has the page and view
   grammar, filters and sorts, rich text, forms, document templates, every
   field type with its configuration as JSON Schema, the formula functions,
   and the connector's tools by name. Fetch it when you need it, never from
   memory and never from a copy:
   - read `https://api.atome.sh/docs/atome-grammar/version` first, and say which build you read (`build_sha`);
   - then the page that covers the question; `https://api.atome.sh/docs/atome-grammar/llms.txt` lists them;
   - if a fetch fails, say so plainly and stop rather than guess.
3. **Atome's own playbooks.** `load_playbook` without an id lists them (the
   interface-building one, the workflow-builder one for automations). They
   are not in the published grammar; they come from Atome's server and are
   always current: when one says something precise, it wins.
4. **The tools' own descriptions.** Each Atome tool says what it takes and
   who may call it (many structure tools need an owner or an admin, and the
   connection's write access to pages and automations); `https://api.atome.sh/docs/atome-grammar/tools/index.md`
   lists them all, one line each.
5. **The reference files here**, for what has bitten before: rules proven on
   a real Atome workspace, each with its id and its status. They do not
   repeat the published grammar; when they differ from it, the published
   page says what the running build accepts.

## Which reference to read

Read only the family you touch.

| The question is about | Read |
|---|---|
| a field, its type, its configuration; relations, lookups, rollups; collections | [fields](reference/fields.md) |
| a formula, a date calculation, a reference inside a workflow | [formulas](reference/formulas.md) |
| a view, a filter, a page and its publication, a form | [views, pages, forms](reference/views-pages-forms.md) |
| a workflow, its trigger and steps; an agent and its skills | [workflows and agents](reference/workflows-and-agents.md) |
| records: importing, updating, keys, errors | [records](reference/records.md) |
| who sees what; the company brain | [access and context](reference/access-and-context.md) |

Each rule reads `ID (status): rule`. **Proven**: tried on a real Atome
workspace. **Probed**: seen on a real workspace by reading only. **Read**:
read in Atome's code, not yet tried. **Open question**: asked to Atome's
engineers, not settled; say so when you rely on it.

## The golden rules

1. **What Atome serves is the truth.** A type, a step, a layout exists only
   if Atome's published grammar, its tools and its playbooks accept it.
2. **A rule has its source.** Without one, it is a question, not a rule.
3. **Nothing goes live unchecked.** A view is written as a draft, validated,
   then published; a workflow is a draft until it is published; a form
   collects nothing until it is published.
4. **A write that replaces is sent whole.** A field's configuration, access
   rules in replace mode, a brain file: read, change, send everything back.
5. **Read before writing, and read back after.**
6. **What has no way back is done by the person in Atome**: deleting a
   collection or a field, merging records, regenerating a public link.

## When a tool fails

When an Atome tool fails or needs a workaround, offer to report it to
Atome's team with `report_issue`, through the atome-retour skill: drafted,
shown, and sent only on their yes, never with their data.
