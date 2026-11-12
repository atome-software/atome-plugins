# Formulas and references

What has bitten before with a formula field and a workflow reference.
Each rule: `ID (status): rule`. The functions a formula may call, with their
signatures, are Atome's published page `https://api.atome.sh/docs/atome-grammar/formulas/functions.md` (read
`https://api.atome.sh/docs/atome-grammar/version` first and say which build you read).

## Formula fields

- **CH-012 (proven)**: a formula has its expression, the list of fields it
  reads, and its return type (number, text, boolean, date, relation, select,
  multi-select, any). All three are required.
- **EX-001 (read)**: a formula reads a field with `prop("slug")`.
- **EX-006 (proven)**: a formula calls only the functions of the published
  page (`https://api.atome.sh/docs/atome-grammar/formulas/functions.md`), with the signatures it gives. The 77
  functions Atome had on 29 Oct. 2026 were each tried on a real workspace.
- **EX-008 (proven)**: a formula in error is empty, without saying so. Read
  its value on a record before relying on it.

## Dates

- **EX-007 (proven)**: `dateAdd(date, number, unit)` and
  `dateBetween(start, end, unit)`: the date first, then the number, then the
  unit. Units are plural: days, weeks, months, years, hours, minutes,
  seconds. `"day"` raises no error, but `dateBetween` then returns
  milliseconds and `dateAdd` nothing.
  - "the number of days between the start and the due date":
    `dateBetween(prop("start"), prop("due"), "days")`, return type number;
    it gives due minus start, positive when the due date is later.
  - "thirty days after the start": `dateAdd(prop("start"), 30, "days")`,
    return type date.
- **EX-013 (proven)**: dates are calculated in UTC: `today()` is midnight
  UTC. To show a time in Paris:
  `formatDate(setTimezone(now(), "Europe/Paris"), "HH:mm")`. What
  `setTimezone` returns never goes back into `dateAdd` or `dateBetween`.
- **EX-014 (proven)**: a gap is a number formula, a due date a date formula,
  a date as text a text formula; the value is calculated after the record is
  written: read it back, do not assume it.

## References inside a workflow

- **EX-003 (proven)**: a reference starts from `trigger` (the record or
  message that started the run), `steps.<id>` (what an earlier step
  returned) or `system.now`. A record's own fields sit under their field id:
  `trigger.<field id>`.
- **EX-004 (proven)**: a reference is written as a formula reference, never
  `{{…}}`, which would stay written as is.
- **EX-005 (proven)**: a reference that ends on a record is a relation; its
  `.id` is a text. A relation to the record that started the run is
  `prop("trigger.record")`, never its `.id` (WF-014).
- **EX-011 (proven)**: a search returns a list: `steps.<id>.length` for its
  count, `steps.<id>.0` for the first record. There is no `first` and no
  `count`.
- **EX-012 (proven)**: inside a loop, the current item is
  `steps.<loop>.element` and its rank `steps.<loop>.index`.
- **EX-002 (proven)**: in a workflow filter, a condition whose value is
  empty is silently dropped; with no condition left, a search returns records
  from the whole collection. Never leave a condition without a value.
