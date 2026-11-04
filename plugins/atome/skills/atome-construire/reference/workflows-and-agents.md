# Workflows and agents

The grammar of a workflow is Atome's workflow-builder playbook
(`load_playbook`): load it before writing one. These are the rules that have
bitten before. Each rule: `ID (status): rule`.

## Triggers

- **WF-003 (probed)**: the triggers: manual, scheduled, record_created,
  record_updated, record_deleted, record_matches_condition, webhook,
  email_received, email_sent, email_thread_updated,
  email_thread_matching_condition, form_submitted, booking_event,
  external_message_received, campaign_event.
- **WF-007 (proven)**: a button is a manual trigger (source button, with its
  collection); a schedule has its frequency, its time and its time zone
  (`Europe/Paris`; UTC otherwise); a record trigger has its collection, and
  record_updated the fields that count.
- **WF-020 (proven)**: record_matches_condition fires when a record turns
  true for its filter, on creation or update; a record that stays true does
  not fire it again.
- **WF-021 (read)**: a record_updated workflow that writes on its own record
  starts itself again. Watch only fields it does not write.
- **WF-019 (proven)**: record triggers run a few seconds after the write, in
  a queue.

## Steps

- **WF-008 (proven)**: a step is `{id, type, …its own keys}`.
- **WF-010 (proven)**: seven step types publish but never run: the three
  meeting steps, filter_records, sort_records, switch_values and
  custom_code. A workflow does not use them.
- **WF-011 (proven)**: a create, update or delete step returns only the id of
  the record and its collection; read a field of a created record with a
  get_record step after it.
- **WF-013 (proven)**: a step writes a field by its id, never its slug; a
  select by the id of its option.
- **WF-014 (proven)**: a relation to the record that started the run is
  `prop("trigger.record")`.
- **WF-022 (proven)**: a branch is not an if/else: every branch whose
  condition is true runs, in order, and a branch without a condition always
  runs.
- **WF-002 (probed)**: the step that prepares an email without sending it is
  create_draft.
- **WF-012 (read)**: what a step does outside the workspace: send_email,
  forward_email, send_whatsapp_template and call_api really send; the AI
  steps cost AI credits; notifications, channel messages and approvals reach
  members.

## Publishing and running

- **WF-016 (proven)**: publishing freezes a copy; later edits are a draft
  and the previous version keeps running until the next publication.
- **WF-017 (proven)**: unpublishing stops it and keeps its copy.
- **WF-023 (proven)**: a schedule runs at its time from its publication, in
  the name of whoever published it.
- **WF-029 (read)**: a run acts in the name of whoever started it (who
  clicked, who wrote the record), otherwise the workflow's author. What that
  member cannot see, the run cannot see.
- **WF-028 (read)**: limits: 50,000 runs a month per workspace (beyond that,
  runs are skipped without a trace); ten tries per step, then the run fails;
  a search returns 50 records by default.

## Agents

- **AG-002 (proven)**: an agent is born a draft, in suggest mode.
- **AG-005 (proven)**: an agent needs its persona and its data scope; access
  per collection is none, read, write or ask (a write that waits for
  approval).
- **AG-006 (proven)**: the data scope names collections by slug, and nothing
  checks they exist: read them with `describe_collection` first.
- **AG-008 (read)**: activating an agent creates its member in the
  workspace (a bot that signs its messages). Only on the person's words.
- **AG-010 (proven)**: an agent's skill is a file of the brain:
  `skills/<slug>.md` for the team, `agents/<id>/skills/<slug>.md` for one
  agent.
- **AG-011 (proven)**: with no skills chosen, an agent has the team's whole
  menu; with a list, only those, plus its own.
- **AG-012 (read)**: an agent sees only a skill's name and description when
  choosing: without a description, a skill is never loaded.
- **AG-013 (read)**: run by a workflow, each agent run is a paid turn; with
  no human to confirm, an agent in suggest mode, or a collection in ask
  mode, writes nothing and says what it would have done. Compose the
  approval: run the agent, then wait for an approval.
- **AG-016 (read)**: a file attached to an agent becomes readable by
  everyone who uses it.
