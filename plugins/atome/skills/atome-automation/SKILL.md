---
name: atome-automation
description: Make something happen on its own in an Atome app, said in the person's own words, through Atome's connector. Workflows on a record, a form, an email, a button or a schedule, and agents that propose. « Automatise un mail quand un deal est gagné », « préviens-moi quand un nouveau contact arrive », « relance le client si le devis n'est pas signé après 7 jours », « envoie-moi chaque lundi les deals sans activité », « quand le formulaire est rempli, crée la société et le contact », « un bouton qui envoie le contrat », « un agent qui propose la prochaine étape de chaque affaire ». Use it whenever a request says when, as soon as, every week, on its own, automatically, a reminder, an alert, a notification, an automatic email, a workflow or an agent.
---

# Your Atome app: what happens on its own

The person says what should happen on its own. You set it up in their app as
a workflow (or an agent that proposes), through Atome's tools, showing first
what will happen and when. Talk about their app (the deal that is won, the
email that goes out), never about tools or payloads. Answer in the person's
language.

## Before anything

1. **The workspace** and **their company** as for any change of their app
   (the atome-interface skill, "Before anything").
2. **Atome's workflow-builder playbook**, always, before writing a workflow:
   `load_playbook` without an id lists them; load the one for automations.
   It is the grammar `create_workflow` and `validate_workflow` enforce.
3. **The rules that have bitten before**: the atome-construire skill,
   `reference/workflows-and-agents.md`.

## The round

1. **The trigger, in their words.** A button, a record created or changed or
   that starts meeting a condition, a form received, an email received, or a
   fixed time. Never on a calculated field: check it at a fixed time instead.
   Say it back: "when X, then Y".
2. **One logic, thin entries.** The logic lives once; each button or inbox is
   only a way into it (one workflow, several triggers).
3. **No duplicates.** Look for a key (an email's thread, a record's id)
   before any creation step.
4. **The agent proposes, the person validates.** An agent writes only its own
   column or its proposals.
5. **An email leaves from their mailbox**: as a draft first, until they have
   seen a first real one.

## Setting it up

1. **Read live**: `list_workflows` (and `get_workflow` for one that exists),
   `describe_collection` for the field ids the steps will write.
2. **Draft it**: `create_workflow` always makes a draft that runs nothing.
   Then `validate_workflow`: it checks it the way publishing would. Read every
   issue it lists, fix each step it names (`update_workflow`, keeping the ids
   of what you do not change), validate again. Never retry at random.
3. **Show it**: one or two sentences, "when X, then Y", what it writes and in
   whose name it runs (the person who triggered it, or for a schedule, who
   published it).
4. **Their go, then publish**: `publish_workflow` starts it on real records
   and people. Publishing is its own change, with its own go: "Turn it on"
   (first, recommended), "Change something", "Not now".
5. **Try it for real once per entry**: a button with `run_workflow` (with the
   record it runs on), a record trigger by writing a test record they agree
   on. Then `list_workflow_runs` and `get_workflow_run`: each step's status
   and output.
6. **Stop or pause**: `set_workflow_active` pauses it, `unpublish_workflow`
   stops it and keeps its copy. A workflow cannot be deleted through the
   connector yet: to remove one, unpublish it and tell the person where to
   delete it in Atome.

## What Atome takes in a workflow

- **Field values by field id**, read from `describe_collection`, never by
  their name; an option by its id. A computed value is a formula reference,
  never `{{…}}`, which would stay written as is.
- **A branch is not an if/else**: every branch whose condition is true runs,
  and a branch without a condition always runs. There is no "otherwise".
- **A record-updated trigger that writes on its own record** starts itself
  again: watch only fields it does not write.
- **A record-matches-condition trigger** fires when the record turns true,
  not while it stays true.
- **Publishing freezes a copy**: later edits are a draft until the next
  publish, and the previous version keeps running meanwhile.
- **Steps that publish but never run**: custom code, meeting steps, filter,
  sort and switch steps. A workflow does not use them.
- A schedule has its time zone (`Europe/Paris` for a French team).

## Agents

- `create_agent` makes a **draft**, inert until activated. Its persona is a
  role in a few sentences, not a procedure; leave `steps` empty unless the
  person described an exact sequence. Ground every collection slug of its
  data scope with `describe_collection`: nothing checks they exist.
- It starts in `suggest` mode: it prepares, a person approves. Do not make it
  more autonomous without their words.
- **Activating an agent adds a member to their workspace** (its bot
  identity): only on their explicit words, never as a test
  (`update_agent` with status active).
- **Its know-how goes in skills**: `create_skill` writes one, created
  disabled; the person reviews it, then `update_skill` turns it on. Its
  description is what makes an agent load it: one sentence, the situation.
- **Run by a workflow**, every agent run is a paid turn, and an agent in
  `suggest` mode writes nothing there, with no human to confirm: compose the
  approval (run the agent, then wait for an approval). Say it before
  publishing.

## Done when

- one real run per entry has gone through, and they have seen it (the draft
  email, the task created);
- after turning it on, no run is stuck and none has failed;
- they know what runs, when, and how to pause it.

## When it is really stuck

The same issue twice, or an error the playbook does not cover: report it
with `report_issue` (never record values or personal data), tell the person
plainly what is blocked, and go on with what can be done.
