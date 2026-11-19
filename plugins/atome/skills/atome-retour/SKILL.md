---
name: atome-retour
description: Tell Atome's team what did not work in Atome, through Atome's connector and its report_issue tool, only on the person's yes and never with their data. At the end of a build session, or when the person says something is off, review the session, draft at most three reports (a bug, something blocked, something confusing), show them, and send each one only after their yes. « Ça ne marche pas », « c'est bizarre, signale-le à Atome », « remonte ça à l'équipe Atome », « envoie un retour sur ce bug », « fais le point sur ce qui a coincé ». Use it when a build session ends, when an Atome tool fails or needs a workaround, or when the person wants Atome's team to hear about a problem.
---

# Telling Atome's team what went wrong

Atome's team fixes what its connector does badly once it hears about it.
Atome's `report_issue` tool sends them a short report: what was tried, what
was expected, what happened. You turn a session's hiccups into at most
three clear reports, show them, and send each one only on the person's yes.
Their data never goes in: a report describes the shape of the problem.
Answer in the person's language, from your first message (in French, always
« vous », even when they write « tu »).

`report_issue` changes nothing in their app, and works on a read-only
connection too. It is the only Atome tool this skill calls.

## When

- **At the end of a build session** (the atome-interface, atome-automation
  or atome-migration skills): if an Atome tool failed, refused, or needed a
  workaround during the session, offer it once, in one line, after the
  summary of what was built. If nothing went wrong, say nothing.
- **When the person says something is off**: « ça ne marche pas », « c'est
  bizarre », « signale-le à Atome ».
- **When another skill hits a failure or a workaround**: finish helping
  first, then offer.

Not for the person's own mistake (a typo, a choice they corrected), nor
for a refusal that comes from the access they granted when they connected:
explain that one instead (which access, and that they change it when they
connect again).

## Review the session

Go back over this conversation, the calls you made and what Atome answered:

1. each Atome tool that returned an error or a refusal you could not get
   past;
2. each workaround you needed: a second call, another tool, a step the
   person did by hand in Atome;
3. each tool that behaved differently from its description;
4. each thing the person asked for that Atome's tools cannot do.

The same problem seen twice is one report. Keep the three that would help
most: the ones that blocked the person, came back, or cost them a step by
hand. Atome merges duplicates on its side, so one report per distinct
problem is enough.

## Each report

The tool's own fields and kinds:

| Field | What goes in |
|---|---|
| `kind` | `bug`: a tool errored or misbehaved. `blocked`: what they asked is impossible with the tools available. `confusing`: a tool works differently from its description. |
| `tool` | the Atome tool concerned, when there is one (`update_field`, `create_workflow`…); 100 characters at most |
| `title` | the skill, then the problem in a few words; 120 characters at most. For example `atome-interface: update_field drops the option groups of a select field` |
| `expected` | what you were trying to do and what you expected; 1000 characters at most |
| `actual` | what happened instead, with Atome's exact error message; 2000 characters at most |

Pass the workspace's slug as `workspace`, as for any call (`list_workspaces`
first if you do not have it yet). Write in English or in French: Atome's
team reads both.

## Their data stays out

A report carries the shape of the problem, never the person's data. Before
you show a draft, take out:

- **names**: of people, companies and records, and of their own
  collections, fields, pages and workflows. Say "a custom collection", "a
  select field with six options", "a relation to contacts" instead;
- **values**: what a field holds, an email address, a phone number, an
  amount, a date that belongs to a record;
- **record contents**: rows of a file, the body of an email or a message,
  a note, a transcript; and the ids of their records.

Atome's error message goes in as Atome wrote it, with any name or value in
it replaced by its shape (`<a contact's email>`, `<a record name>`). What
the team needs stays: Atome's tool names, field types, the native
collections (contacts, companies, tasks), the keys of the input and how
many rows it had.

Say it in one line with the drafts: "I removed names, values and record
contents: Atome's team sees the shape of the problem, never your data."
(« J'ai retiré les noms, les valeurs et le contenu des fiches : l'équipe
d'Atome voit la forme du problème, jamais vos données. »)

## Show, then send on their yes

1. **Show the drafts** exactly as they will be sent, numbered: kind, tool,
   title, expected, actual. Then the line about their data.
2. **Ask** in one question: "Send them" (first, recommended), "Change
   one", "Don't send". A yes counts for the reports it names: « envoie les
   trois » sends the three, « envoie le premier » sends only the first. A
   bare « ok » with several drafts: ask which ones. A no, no answer, or a
   change of subject: nothing is sent.
3. **Send** each report they said yes to with `report_issue`, as shown. A
   draft they changed is shown again before it goes.
4. **Read the answer** and say it plainly: `reported` means Atome's team
   has it; `already_reported` means they already had it, and `occurrences`
   says how many times it has now been seen. An error ("too many
   submissions", "reporting is unavailable right now"): say so, keep the
   draft, and offer to send it later. Never retry in a loop.
5. **Carry on** with what the person was doing. Do not promise a fix or a
   date: Atome's team decides.

## What this skill never does

- Send a report without the person's yes, or more than three drafts from
  one review.
- Put their data in a report, or ask them for any to add.
- Report their own mistakes, or a refusal that comes from the access they
  granted.
