---
name: atome-interface
description: Change what people see and enter in their Atome app, said in their own words, through Atome's connector. Fields, columns, option lists, collections, views (kanban, table, calendar), pages, dashboards, forms, buttons, and who sees what. « Ajoute un champ statut à mes projets », « renomme la colonne Description », « crée une vue kanban de mes deals par étape », « une vue calendrier des rendez-vous », « fais une page d'accueil pour l'équipe », « un formulaire pour demander un devis », « une collection pour suivre mes fournisseurs », « que les commerciaux ne voient que leurs deals ». Use it whenever a request touches a field, a column, an option list, a collection, a view, a page, a form, a button or access in Atome.
---

# Your Atome app: what people see and enter

The person says what should change in their app. You make it, one change at
a time, through Atome's tools, showing first what will change. Talk about
their app (their projects, their deals, their page), never about tools,
payloads or ids. Answer in the person's language (French when they write in
French).

Every write goes through Atome's own tools, under the access the person
granted when they connected Atome. There is nothing to install, no key and no
script.

## Before anything

1. **The workspace.** If the connection reaches several workspaces
   (`list_workspaces`), ask which one once, then pass it to every call.
2. **What Atome already knows of their company**: read `company/profile.md`
   with `read_brain_file`. If it is missing or thin, do the welcome first
   (the atome-accueil skill), in a few questions, then come back to the
   request.
3. **The grammar of what you touch**, before writing. For a page, a view or
   a form: Atome's interface-building playbook (`load_playbook` without an
   id lists them; load the one for pages and views). For the rules that have
   bitten before: the atome-construire skill and its reference files
   (`fields.md`, `views-pages-forms.md`, `access-and-context.md`).

## One change

1. **Read live, never from memory.** `list_collections`, then
   `describe_collection` (with `raw: true` before changing a field: it gives
   each field's stored shape), `list_pages` and `get_page_view` for a page,
   `get_access_rules` for access. Find the collection, field or page they
   mean; if two things look like it, ask which one.
2. **Say it in one sentence**: what will change and where they will see it.
   For a field whose configuration you replace, keep the configuration you
   read: it is the only way back.
3. **Ask for the go**, as a question with clear choices: "Make this change"
   (first, recommended), "Change something", "Cancel". Any go in their own
   words (oui, go, vas-y, fais-le) counts. On "Cancel" or a no, nothing is
   written. One go, one change.
4. **Write**, then **read it back** (`describe_collection`, `get_page_view`,
   `get_access_rules`). A success message is not a proof; the read-back is.
5. **Check the screen with them**: where to look in their app, what they
   should see there.
6. **Say how to undo it**, plainly: a page view comes back with the previous
   view that `update_page_view` returned; a field comes back with the
   configuration you kept; access comes back with the rules you read. Record
   writes have `undo_change`. If they say « annule ce changement », do it
   right away.

## Fields and collections

- **A field's configuration is replaced whole** by `update_field`: read it
  first, change what was asked, send everything back. A missing key is lost
  (its options, the other side of a relation).
- **Status** fields have three groups of options (to do, in progress,
  complete); a new status gets only the options you give it. **Select**
  options sit in groups; changing an option's label keeps its id, so views
  and filters that use it keep working. Never rebuild options to rename one.
- **A relation is created from one side only**: Atome creates its mirror in
  the other collection. Creating both sides makes two relations.
- **Order**: the target collection, then the relation, then a lookup or a
  rollup that reads through it, then a formula that reads them.
- **Native collections** (companies, contacts, tasks, projects, members) are
  extended, never recreated. A new collection comes with its Name and Files
  fields and its record page: do not create them again.
- **Retyping a field** can lose the values the new type cannot hold: say so
  before, and ask.

## Pages, views and forms

- Load the interface-building playbook first; it is the grammar the
  validators enforce.
- **A page is visible as soon as it exists**, and it cannot be unpublished,
  only deleted. Create it only once the person wants it, then write its view
  as a draft (`update_page_view`), check it with `validate_page_view`, show
  what it will look like, and publish with `publish_pages` (its `page_ids`)
  after their go. `publish_pages` without `page_ids` publishes nothing and
  lists the pages with unpublished changes.
- **Filters on a select or a status use option ids**, never labels. A count
  or a rollup with no link is empty, not 0: filter it with "is not empty".
- **A form is created as a draft** (`create_form`) and collects nothing until
  `publish_form`. A form that creates records must ask for every required
  field and the record's name. Publishing is its own change, with its own go.

## Who sees what

`update_access_control` shows the impact first (`dry_run` is true by
default): who loses access, who gains it, how many records. Show the person
who loses access, and only after they agree, call it again with `dry_run`
false. `mode: "replace"` overwrites every rule of the collection: read them
with `get_access_rules` first. Whoever created a record or was sent it always
keeps it.

## A build: one plan, one go

When the request is more than one small change (« monte-moi le suivi des
projets »: several collections, their fields, a page, an automation), do not
make them approve each write.

1. **Read live** what already exists, so nothing is created twice. Ask only
   what Atome and their profile do not settle, three questions at most, the
   recommended answer first (the atome-accueil skill, "Before a build").
2. **Write the whole plan in your message**, short, grouped in three to six
   lines, for example:

   > Here is what I will do in your app:
   > - a "Deals by stage" page, published for the team;
   > - on it, your deals as a kanban, one column per stage;
   > - your deals and their fields do not change.

3. **One go for the whole plan**: "Build it now" (first, recommended),
   "Change the plan", "Cancel". On the go, run it to the end in the same
   turn, in order (targets before relations, relations before lookups,
   formulas last, publications last), reading back each step.
4. **Stop only for a real doubt**: a field that already holds values, what
   they meant cannot be found, a change to existing things the plan did not
   name, an error the grammar does not cover. Ask, in plain words, then go on.
5. **At the end**: what was built, where to see it, what can be undone and
   how. Then offer to write what was built and decided back to Atome (the
   atome-accueil skill, "Writing back to Atome").

## What Claude does not do here

These have no way back, so the person does them in Atome themselves, and
you tell them where to click: deleting a collection or a field, merging
records, regenerating a form's public link. Never put a key, a token or
record values beyond what the change needs in the chat.

## When it is really stuck

The same error from Atome twice, or an error the grammar does not cover and
a retry does not pass: do not go round in circles. Tell the person in plain
words what is blocked. Big builds and large imports go through an Atome
consultant: say so, and point them to Atome's support.

When an Atome tool fails or needs a workaround, offer to report it to
Atome's team with `report_issue`, through the atome-retour skill: drafted,
shown, and sent only on their yes, never with their data.
