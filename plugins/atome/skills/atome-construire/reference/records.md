# Records: writing, importing, keys

What Atome takes when records are written in bulk (`update_records`,
`create_records`). Each rule: `ID (status): rule`. `describe_collection`
with `raw: true` says what each field accepts and the keys rows can be
matched on.

## A batch

- **FI-002 (proven)**: a batch holds 1 to 500 rows of one collection, keyed
  by field key, with one answer per row, in order.
- **FI-003 (proven)**: a refused row does not sink the batch: it alone fails,
  with its reason, and the other rows are written.
- **FI-015 (proven)**: with `atomic: true`, one refused row cancels the whole
  call.
- **FI-019 (proven)**: a dry run checks everything (keys, values, options,
  targets, uniqueness, matching) and writes nothing. Always run it first.
- **FI-004 (proven)**: a refused row carries one of fifteen codes, each with
  a hint: field_unknown, field_read_only, field_forbidden_for_actor,
  value_invalid, value_required, option_unknown, relation_target_not_found,
  relation_cycle, unique_violation, duplicate_in_batch, match_value_missing,
  match_ambiguous, row_forbidden, batch_rolled_back, internal. Act on the
  code, not the message.

## Keys and re-runs

- **FI-012 (proven)**: the match key is one field: a unique text, url,
  email, phone or number field, or the `external_id` field even if not
  unique, or `id` (update only, never create). Create `external_id` once, as
  a unique text field.
- **FI-013 (proven)**: matching ignores case and surrounding spaces; each
  row comes back created, updated or unchanged. Running the same batch again
  changes nothing: that is how an import resumes.
- **FI-014 (proven)**: two rows with the same key in one call: the first
  wins, the second is skipped. A row without a key fails. Several existing
  records with the same key: the row fails as ambiguous.
- **FI-016 (proven)**: matching on `id` updates several fields of a record in
  one call and never creates.

## Values

- **FI-006 (proven)**: a select or a status takes an option's id or label,
  any case; a multi-select a list of them. A label two options share is
  refused.
- **FI-007 (proven)**: a number may come as a string; a boolean as true,
  false, 1, 0, yes, no; a date as ISO 8601 or DD/MM/YYYY (kept at midnight
  UTC); rich text as a plain string, wrapped in a paragraph.
- **FI-008 (proven)**: progress from 0 to its max; a scale a whole number up
  to its max; an email name@domain.tld; a phone at least six digits, a
  leading + allowed.
- **FI-030 (proven)**: a duration is `{value, unit}` (minute, hour, day), or
  a number of hours.
- **FI-009 (proven)**: lookups, rollups, formulas and ledgers are not
  written: Atome calculates them.
- **FI-010 (proven)**: a relation takes the ids of its target records: create
  the targets first, then link.
- **FI-029 (proven)**: a required field is checked on creation only.
- **CA-015 (proven)**: in one batch, a row without a link placed before a
  linked row leaves the linked row's lookups and rollups empty: put linked
  rows first, or write each kind of row in its own batch.
- **FI-011 (proven)**: calculated fields are computed after the answer: read
  them back, do not read them from the write's result.

## Afterwards

- **FI-018 (proven)**: a deleted record is soft-deleted and can be restored;
  a company or contact absorbed by a merge cannot.
- Each record write over the connector has a `change_id`: `undo_change`
  reverses it once, and `list_my_changes` lists them for 30 days.
