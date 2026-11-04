---
name: atome-migration
description: Bring data from elsewhere into an Atome app without losing or inventing any, through Atome's connector. An export from HubSpot, Pipedrive, Airtable, Notion or Excel, a CSV file, a list of clients, then the duplicates. « Importe mes contacts depuis un export HubSpot », « on quitte Airtable, récupère nos bases », « j'ai un fichier Excel de 2000 clients, mets-les dans Atome », « reprends nos deals de Pipedrive », « un CSV à charger », « fusionne les doublons après l'import ». Use it whenever a request talks about importing, migrating, loading, moving data, an export, a CSV or Excel file, or a tool being left for Atome.
---

# Bringing their data into their Atome app

The person wants data from somewhere else to live in their app. The goal:
every row of the export ends up in Atome, and the check measures it at
**zero gap**. Nothing is written before it has been tried: the file first,
then a dry run, then the real write, then the check. Answer in the person's
language.

This is for the everyday import: a few hundred or a few thousand rows, one
collection at a time. A large migration (tens of thousands of rows, many
linked tables, a whole tool to leave) goes through an Atome consultant: say
so early, and point them to Atome's support.

## First, with them

1. **The workspace** and **their company**, as for any change (the
   atome-interface skill, "Before anything").
2. **The export**: a file they share in the conversation (CSV, or Excel
   saved as CSV), or a file already in Atome (`read_file`, `analyze_file`
   for a PDF). It needs a column that identifies each row in the tool it
   comes from (its "Record ID", "id"…). Read it; do not copy its rows into
   your answers beyond a few examples.
3. **Where it goes.** Each file finds its collection (one that exists, or a
   new one, created first with the atome-interface skill), each column its
   field, in Atome's types (the atome-construire skill, `reference/fields.md`).
   `describe_collection` with `raw: true` says what each field accepts and
   `match_on`, the keys rows can be matched on.
4. **A key for re-runs.** The collection gets a unique text field
   `external_id` (`create_field`, `is_unique: true`) holding the source id:
   the same file can then be loaded again without creating duplicates.

## The round

1. **The mapping, said back**: "your column X goes to the field Y", in a
   short list, and what is left out. Ask for their go on it.
2. **The dry run**: `update_records` with `match_on: "external_id"`,
   `dry_run: true`, up to 500 rows per call. It says what would be created,
   updated, unchanged, and every refused row with its reason. Fix a refused
   row in the mapping, not in Atome.
3. **Their go on the counts**, then the real call, batch by batch, the same
   rows without `dry_run`. Rows that match existing records update them, and
   their previous values would not come back by themselves: say so before.
   For an import, ask whether Atome's automations should fire on these
   records; if not, `skip_automations: true` (workspace admins only).
4. **Relations**: create the target records first, then link by their ids.
   In a batch, put the rows that carry a link first: a row without a link
   placed before a linked row leaves the linked row's lookups and rollups
   empty.
5. **The check**: the number of rows in the export, the number of records in
   the collection, and a few records read back one by one (`read_record`).
   Zero gap, or it is not finished.

## Going back

Each record write returns a `change_id`; `list_my_changes` lists them for 30
days. `undo_change` reverses one: fields return to their old values, created
records are deleted. A field someone edited since is left alone and
reported. Tell them this before the first real batch.

## Duplicates

`find_duplicates` finds companies or contacts that look alike (same domain,
email, phone or name), with the record a merge would keep. These are
suggestions: check each group with the person. Merging has no way back, so
they merge in Atome themselves; you tell them which groups and where.

## The safeguards

- Their data stays between them and Atome: no copy elsewhere, no rows in a
  report.
- Nothing is fixed by hand in Atome: fix the mapping, run it again.
- No key in the chat: the connection is the one they signed in with.

## When it is really stuck

The same refusal twice, or one the field rules do not explain: report it
with `report_issue` (the shape of the row, never its values), tell them
plainly what is blocked, and offer the consultant route for this import.
