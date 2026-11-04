---
name: atome-accueil
description: Get to know the person's company from what Atome already knows of it, then keep Atome up to date with what is learned and built together, through Atome's connector. « On commence », « qu'est-ce que tu sais de mon entreprise ? », « voici qui on est », « notre cycle de vente », « mets Atome à jour avec ce qu'on a fait », « garde ça dans le contexte d'Atome ». Use it at the first working session on their Atome app, when they talk about their company, their team or their sales cycle, before a build, and at the end of a build to write back to Atome.
---

# Getting to know them, then keeping Atome up to date

Atome already knows a lot about their company: its brain (the context
Atome's own agent reads), its collections and their stages, its team. Read
it first, tell them what you understood, let them confirm or correct, and
ask only what is left. At the end, what was learned goes back into Atome, so
that everyone (their colleagues, Atome's agent) starts from the same thing.
Answer in the person's language (vouvoiement in French).

## If Atome's tools are not there

The plugin brings Atome's connector, but the person signs in. In Claude
(web, desktop): Customize, Connectors, Atome, Connect. In Claude Code: run
`/mcp`, choose atome, Authenticate. Atome's consent page asks which
workspace and what access: reading is enough to start; building needs write
access to records and to pages and automations. Never ask them for a key.

## The welcome, the first time

1. **Read, and say so.** Nothing is written.
   - `list_workspaces`, then the map Atome generates of their app:
     `read_brain_file` on `workspace/index.md`;
   - what their team wrote: `company/profile.md`, `company/glossary.md`,
     `company/processes/` (`list_brain_files` to see what exists);
   - `list_collections`; the stages of their cycle are the options of the
     stage field of their deals collection (`describe_collection`), not in
     the brain;
   - `list_member_groups` for how their team is organised.
2. **Say what you understood**: one short card per theme (their business,
   their sales cycle, their team, their tools), each marked "read in Atome"
   or "to confirm". No tools, no paths.
3. **Confirm line by line**: for each "to confirm" card, one question with
   "Right" or "Correct it". On "Correct it", ask what is wrong and say the
   corrected line back ("Noted: …").
4. **Then only what is missing**: three questions at most, the most blocking
   first, the recommended answer first, in one go. What Atome already
   settles is never asked again; beyond three, the recommended answer
   stands and you say it in one line.
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

What was learned (the profile they confirmed), decided and built goes into
Atome's context: `company/profile.md` (their company),
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
- Never in `rules/`: Atome's agent reads it in every conversation, for
  everyone. Never in a member's profile, nor in the text of the
  organisation's emails.
- No key, and no record values in an answer beyond what the summary needs.
