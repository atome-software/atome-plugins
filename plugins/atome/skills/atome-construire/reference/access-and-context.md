# Access and the company brain

Who sees what, and what Atome knows of the company. Each rule:
`ID (status): rule`.

## Access

- **AC-001 (probed)**: a collection is private (rules grant access) or
  public (rules hide records); public may be view only, where everyone reads
  and only participants edit. Without any configuration, companies and
  contacts are private, every other collection public.
- **AC-002 (proven)**: replacing access rules replaces every rule of the
  collection, guest rules included: read them first, merge, send them all
  (`update_access_control` with `mode: "replace"`), or add with
  `mode: "add"`.
- **AC-010 (proven)**: owners and admins follow the rules like everyone
  else; but a member always sees a record they created, were sent, or that
  was opened to the whole workspace.
- **AC-012 (read)**: a guest sees only through guest rules, which always
  grant.
- **AC-009 (read)**: "this member's records" is written one way: a relation
  to members that contains the current user, or a relation that matches the
  member's own field (each person sees their own company's records).
- **AC-011 (read)**: outside their rules, a list simply does not show the
  records; opening one gives an access error.
- **AC-013 (read)**: access is set on custom collections, companies,
  contacts, tasks, projects, notes and email threads; files have none.
- **AC-020 (read)**: member groups belong to admins; a rule names a group
  through the members' groups field, sub-groups included.

## The company brain

- **CX-001 (proven)**: the brain is a tree of markdown files: `workspace/`
  (the map Atome generates of the app), `company/` (profile, glossary,
  processes), `rules/`, `skills/`, `topics/`, `members/<id>/` (private),
  `agents/<id>/`.
- **CX-003 (proven)**: `workspace/` is generated from the app; it lists
  fields but not the options of a select or a status. Never write there.
- **CX-004 (proven)**: the stages of a cycle (sales, project, hiring) are the
  options of the select or status field that carries them, in order.
- **CX-008 (proven)**: a brain path is lowercase, ends in `.md`, has at most
  five segments, and starts with one of the folders above.
- **CX-009 (read)**: Atome's agent reads every `rules/` file in every
  conversation, and `company/` and `topics/` when it needs them. A company's
  profile goes in `company/profile.md`, what was built in `topics/`; nothing
  in `rules/`, which would speak to everyone at every turn.
- **CX-005 (proven)**: writing a brain file writes the whole file; owners and
  admins only, outside one's own member folder. Read it first and keep what
  the team wrote.
- **CX-011 (read)**: the organisation's email context is a single text used
  for writing emails; Atome's agent does not read it. A profile goes in the
  brain.
