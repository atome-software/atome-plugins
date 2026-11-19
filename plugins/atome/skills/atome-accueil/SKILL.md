---
name: atome-accueil
description: Get to know the person's company from what Atome already knows of it, then keep Atome up to date with what is learned and built together, through Atome's connector. « On commence », « qu'est-ce que tu sais de mon entreprise ? », « voici qui on est », « notre cycle de vente », « mets Atome à jour avec ce qu'on a fait », « garde ça dans le contexte d'Atome ». Use it at the first working session on their Atome app, when they talk about their company, their team or their sales cycle, before a build, and at the end of a build to write back to Atome.
---

# Getting to know them, then keeping Atome up to date

Atome already knows a lot about their company: its brain (the context
Atome's own agent reads), its own record among their companies, its
collections and their stages, its members, the address of their app; their
website says the rest. Read all of it first, tell them in one short summary
what you understood, let them correct it in one reply, and ask only what is
left. At the end, what was learned goes back into Atome, so that everyone
(their colleagues, Atome's agent) starts from the same thing.

## The five rules of the welcome

1. **Their language, from the first word.** Your first message, and every
   one after it, is in the language the person writes in, even though this
   skill and Atome's tools are in English. A French message never gets an
   English reply, not even a first line. In French, always « vous », even
   when they write « tu », in every message and every skill of the plugin.
2. **The connection first, in one message.** Your first act is
   `list_workspaces`, before any other Atome tool. If Atome's tools are not
   there, or the call says the connection is missing or has expired, send
   one message with the one
   connect step for the app you are in (below) and nothing else: no
   question about their company, no second step to come. Once connected,
   read at once, without asking anything first.
3. **Their company from its own sources.** The portrait comes from what the
   company says of itself: its website, its own record in Atome, its brain,
   its members' job titles. Never infer a person's role, title or team from
   email traffic (who writes to whom, who is copied, what a thread is
   about): emails say what people do with others, never who they are. A
   role no source states is asked, not guessed.
4. **One short summary to correct.** What you understood comes in one
   message, which they correct in one reply: never card by card, never a
   question per line.
5. **What Atome holds is never asked.** The address of their app, the
   workspace, the members and the stages are read before any question; a
   question whose answer Atome holds is never asked.

## The connection

The plugin brings Atome's connector, but the person signs in. The one
step, for the app you are in:

- in Claude (web, desktop): **Customize > Connectors**, **Atome**,
  **Connect** (or the plugin's **Connectors** tab);
- in Claude Code: `/mcp`, choose `atome`, **Authenticate**.

In the same message, what to choose on Atome's consent page: their
workspace, and the access (reading is enough to start; building needs write
access to records and to pages and automations). Then one line: "Tell me
when it's done." Never ask them for a key, nor whether they want to
connect.

If `list_workspaces` answers with no workspace, the consent page did not
tick one: the same single message, to connect again and tick it.

## What Atome already holds

Read all of it before you say anything about their company. Nothing is
written.

- **The workspace**: `list_workspaces`. When there is one, it is theirs:
  never ask. When there are several, ask once which one, by name. Then pass
  its slug as `workspace` to every call, the first read included, even when
  there is only one: a call without it fails on a connection that reaches
  several workspaces.
- **The address of their app**: `https://<host>/<workspace slug>`, the
  start of any link Atome's tools return (each page's `url` in
  `list_pages`, each hit's `link` in `global_search`). Never ask for it.
  Only when no tool returns a link (a connection without access to pages,
  and nothing found), ask once.
- **The members**: the records of the `organization_member` collection
  (`list_collections`, then `search_records` on it): their names, their job
  titles, who reports to whom. Owners and admins also see the groups
  (`list_member_groups`).
- **Their brain**: the map Atome generates of their app (`read_brain_file`
  on `workspace/index.md`), and what their team wrote: `company/profile.md`,
  `company/glossary.md`, `company/processes/` (`list_brain_files` to see
  what exists).
- **Their company's own record**, when there is one: `search_companies`
  with the workspace's name, then `read_record` on the one that is them: its
  domain, its description, its size.
- **Their cycle**: `list_collections`; the stages are the options of the
  stage field of their deals collection (`describe_collection`), not in the
  brain.

## Their company, from its own sources

1. **Their website first**: the domain of their company's record (or of
   their email address), read with the app's web tool when it has one: the
   home page, the about and team pages. Who founded the company and who
   runs it come from there, as the site says it.
2. **Then Atome**: the brain, their company's record, the members' job
   titles. When the website and Atome disagree, give both in the summary
   and let them choose.
3. **Never from email traffic.** Emails, meetings and their clients'
   records can say what the company sells and to whom; they never say who
   someone is in the company. No title, team or role comes from them.
4. **Unsure, ask.** A person whose role no source states is a question in
   the summary ("I don't know what X does here: what is their role?"),
   never a guess. Without a web tool, say that the website was not read.

## The welcome, the first time

1. **Connect, then read**: the connection (above), then everything Atome
   holds and their website, in the same turn, with one line that says you
   are reading and that nothing is written.
2. **One summary to correct**, in one message: "Here is what I
   understood", five to eight short, concrete lines (their business, their
   sales cycle and its stages by name, their team and who does what, their
   tools, what their app already holds), each with its source
   in plain words ("your website", "Atome", "your team's notes"). No tools,
   no paths. A line no source states is not in it: it is a question.
3. **The questions left, in the same message**: three at most, the most
   blocking first, the recommended answer first. What Atome already
   settles is never asked; beyond three, the recommended answer stands and
   you say it in one line. Then: "Correct what is off and answer in one
   reply; what you leave as it is, I keep."
4. **Their reply**: say back what changed in one line ("Noted: …"), without
   showing the summary again.
5. **Offer to write it back** (below), never silently.

## Before a build: their questions

Before writing the plan of a build (the atome-interface, atome-automation or
atome-migration skills), read `company/profile.md` again, then ask only the
questions this kind of build needs and Atome does not settle:

| They build | Ask about |
|---|---|
| a sales pipeline, follow-ups | the stages, who owns a deal, when a deal is lost |
| projects, missions, orders | the steps, who is assigned, what "done" means |
| quotes, invoices, expenses | numbering, currency, who approves |
| hiring, onboarding, absences | the steps, who sees what |

Three at most, in one go, after a sentence that says what Atome already
knows ("Your cycle and your contacts are already in Atome. Three questions
for this CRM:").

## Writing back to Atome: with their go

What was learned (the summary as they corrected it), decided and built goes
into Atome's context: `company/profile.md` (their company),
`company/processes/cycle-de-vente.md` (their cycle),
`topics/construit-avec-claude.md` (what was built and decided, dated). These
are the paths earlier Atome plugins used: keep them, so nothing is written
twice.

- **Show it first**: two or three lines of what will go into Atome, then the
  question: "Update Atome" (first, recommended), "Change it", "Not now". On
  their go, write it in the same turn, then say it is done.
- **An owner or an admin writes**: `read_brain_file` first, then
  `write_brain_file` with the complete new text. It replaces the whole
  human-written content, so keep every line their team wrote, unchanged, and
  change only your own section. The machine-written zone is never touched.
- **Anyone else proposes**: `propose_brain_change` adds one fact at a time,
  pending until someone in their team approves it. Say it was proposed,
  never that it was saved.
- **Every save is versioned**: a bad write is undone by restoring the
  previous version from the file's history in Atome. Tell them.
- **At the end**, three lines: what was built; what was updated in Atome
  ("your profile and 2 decisions"), which Atome's agent will read when it
  talks about their company; and how to undo it.

## What is never done

- Nothing is written to Atome without their go.
- No person's role inferred from email traffic, and no question whose
  answer Atome or their website already gives.
- Never in `rules/`: Atome's agent reads it in every conversation, for
  everyone. Never in a member's profile, nor in the text of the
  organisation's emails.
- No key, and no record values in an answer beyond what the summary needs.

## When a tool fails

When an Atome tool fails or needs a workaround, offer to report it to
Atome's team with `report_issue`, through the atome-retour skill: drafted,
shown, and sent only on their yes, never with their data.
