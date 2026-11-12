# Fields, relations and collections

What has bitten before with a field, a calculation and a collection. Each
rule: `ID (status): rule`. Every field type and the configuration it takes,
as JSON Schema, is Atome's published page `https://api.atome.sh/docs/atome-grammar/fields/index.md` (read
`https://api.atome.sh/docs/atome-grammar/version` first and say which build you read). Read the field's live
shape with `describe_collection` (`raw: true`) before changing it.

## Types

- **CH-001 (proven)**: the field types are the ones the published page
  lists (`https://api.atome.sh/docs/atome-grammar/fields/index.md`), and no others; multi-select is written with
  a hyphen. long_text, currency, percent, datetime, multi_select and member
  do not exist: use rich_text; number with its number format; date with its
  time option; multi-select; a relation to the workspace members.
- **CH-005 (proven)**: an amount or a percentage is a number with its format:
  `number_format.format_type` is number, currency, percent or bytes, and
  `currency_symbol` gives an amount its symbol.
- **CH-006 (proven)**: a date with a time is a date field with
  `include_time: true`.
- **CH-017 (proven)**: there is no member type: a member is a record of the
  workspace members collection, and a "member" field is a relation to it.
- **CH-013 (proven)**: a scale needs its icon (star, signal, heart, circle,
  chevron) and a max between 1 and 10 (5 by default).
- **CH-015 (proven)**: a progress field says where its value comes from:
  manual (0 to its max), or a relation (the share of linked records whose
  read field is complete).
- **CH-016 (proven)**: a list of texts is an array of strings.
- **CH-014 (proven)**: a ledger (an automatic number) has a format with
  `{seq}` and a reset period (never, yearly, monthly, daily); a yearly reset
  needs a year token (`{YYYY}` or `{YY}`), monthly a year and `{MM}`, daily a
  year, `{MM}` and `{DD}`. Existing records are numbered when it is created.

## Options and statuses

- **CH-007 (proven)**: select and multi-select options sit in
  `groups[].options[]`, each option with its id, label, slug and colour.
  Renaming an option keeps its id; views and filters keep working.
- **CH-008 (proven)**: a status has three groups, of kind todo, in_progress
  and complete, each with its options; the default option is the first of
  todo unless one is named.
- **CH-021 (proven)**: a status created outside Atome's screen gets only the
  options it is given: give it its options in their three groups.
- **CH-020 (proven)**: a multi-select needs at least one option; a select
  may have none.

## Changing a field

- **CH-024 (proven)**: a field's configuration is replaced whole, never
  merged: a key left out is lost (its options, a relation's other side).
  Read it, change what was asked, send everything back.
- **CH-019 (proven)**: Atome barely checks a field's configuration: a wrong
  select, status, relation or rollup configuration is stored as is. Check it
  yourself against these rules before sending.
- **CH-018 (proven)**: the primary field (the record's name) can only be a
  text, a ledger, or a formula returning text or a number.
- **CH-029 (proven)**: the primary field cannot be deleted.
- **CH-028 (read)**: no lookup, rollup or formula on email threads or email
  messages.

## Relations and calculations

- **CA-001 (read)**: the order of creation: the target collection, then the
  relation, then the lookup or rollup that reads through it and the field it
  reads, then the formula that reads them all.
- **CA-002 (proven)**: a relation creates its mirror in the target
  collection by itself.
- **CA-003 (proven)**: never create both sides of a relation: each side
  would be its own relation, with its own mirror.
- **CA-004 (proven)**: a one-way relation (no mirror) is the choice for a
  relation to a native collection you do not want to load, such as the
  members.
- **CA-006 (proven)**: a lookup names the relation it follows; without it,
  it follows every relation to the target.
- **CA-007 (proven)**: a rollup with no link (a count included) is empty, not
  0. Filter it with "is not empty", never "greater than 0".
- **CA-008 (proven)**: a formula lists every field it reads, even from its
  own collection; a field left out reads empty and never recalculates it.
- **CA-013 (proven)**: a formula that names a field that does not exist
  reads empty, without an error. Check every field it names.
- **CA-014 (read)**: deleting a relation removes its mirror too.

## Collections

- **CO-002 (read)**: native collections (companies, contacts, tasks,
  projects, members) exist in every workspace: extend them with fields,
  never create a second one.
- **CO-009 (read)**: the 17 native collections: company, contact,
  email_message, folder, calendar_event, file, email_thread, external_thread,
  task, time_entry, project, note, record_list, campaign,
  organization_member, conversation, message.
- **CO-004 (proven)**: a new collection is born with its Name field, its
  Files field and its record page. Do not create them again.
- **CO-006 (proven)**: deleting a collection removes its pages and every
  relation pointing to it, with their values. That is why the person does it
  in Atome, knowing what goes.
