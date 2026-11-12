# Views, pages and forms

The grammar of a page and its view, of filters and sorts, of rich text and
of a form is published by Atome: `https://api.atome.sh/docs/atome-grammar/pages/grammar.md`,
`https://api.atome.sh/docs/atome-grammar/filters/grammar.md`, `https://api.atome.sh/docs/atome-grammar/rich-text/grammar.md`, `https://api.atome.sh/docs/atome-grammar/forms/index.md`
(read `https://api.atome.sh/docs/atome-grammar/version` first and say which build you read; if a fetch fails, say
so and stop). Then load Atome's interface-building playbook
(`load_playbook`) before writing a page, a view or a form. These are the
rules that have bitten before. Each rule: `ID (status): rule`.

## Views

- **VU-001 (probed)**: a data view's layouts are the ones the page grammar
  lists; a board is the kanban. A map is a chart type, not a layout.
- **VU-002 (proven)**: only the keys of the grammar survive in a view;
  unknown keys are dropped without an error.
- **VU-003 (proven)**: a text block holds rich text as a document, following
  Atome's rich text grammar; plain markdown in its place shows nothing.
- **VU-004 (proven)**: a value outside the grammar is refused when written.
- **VU-005 (proven)**: a filter names a field by its slug or its id; a sort
  and a grouping only by its id. Use field ids everywhere: a renamed slug
  does not break them.
- **VU-006 (proven)**: a select, a multi-select or a status is filtered by
  the ids of its options, never their labels, with the multiselect
  operators (is, is not, is any of, is none of) or empty and not empty. A
  checkbox is tested with is true or is false.
- **VU-007 (proven)**: a published record page gets the default context
  panel (Context, then the assistant and messages tabs, which cannot be
  removed).

## Pages

- **PA-002 (proven)**: a page is visible as soon as it exists. Create it
  when the person wants it, write its view as a draft, validate it, then
  publish.
- **PA-010 (read)**: a page cannot be unpublished; it stays visible until it
  is deleted.
- **PA-003 (proven)**: publishing several pages is all or nothing: one
  blocking error refuses the batch and lists every issue.
- **PA-008 (proven)**: an app page's slug is unique in the workspace; a
  record page's, in its collection.
- **PA-009 (proven)**: renaming an app page without its slug makes a new
  slug from the new name: an old link to it stops working. Keep the slug
  when renaming if links matter.
- **AR-002 (proven)**: a record page never has a parent page.
- **AR-003 (proven)**: deleting a page deletes all the pages under it.
- **AR-005 (proven)**: in the apps menu, a top-level page chooses its group,
  and the pages under it follow.

## Forms

- **FO-002 (proven)**: a form is only checked when it is published: a
  refusal lists every issue and publishes nothing.
- **FO-006 (proven)**: publishing needs the submission mode (standalone,
  create, edit), its collection in create or edit mode, and at least one
  question.
- **FO-007 (proven)**: a create form asks for every required field and for
  the record's name, unless the field is calculated or read only.
- **FO-008 (proven)**: publishing freezes the draft: later edits are a draft
  until the next publication.
- **FO-009 (proven)**: unpublishing closes the form (its public link too)
  without erasing what was published.
- **FO-011 (proven)**: a public link's slug is its secret; regenerating it
  kills the old link for everyone. The person does that in Atome.
- **FO-013 (proven)**: a form shared by public link asks no relation and no
  ledger question, and does not read the member.
- **FO-018 (read)**: a submission starts the workflows triggered by that
  form, in the name of the form's owner, never of the person who answers.
