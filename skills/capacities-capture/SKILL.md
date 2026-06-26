---
name: capacities-capture
description: "Captures the current chat into Capacities as a properly linked object via the Capacities MCP connector. Searches the space for related objects first, then creates a typed note with its object-select properties populated so the result is genuinely wired into the graph, not just text. Use this whenever David says 'send this to Capacities', 'capture this', 'save this chat to Capacities', 'add this to my second brain', 'note this in Capacities', or otherwise wants a conversation, decision, or idea preserved in Capacities. Trigger even if he doesn't name the object type or the links explicitly, the skill handles that."
---

# Capacities Capture

Turn a chat into a single, well-linked object in David's Capacities space. The connector is the hands; this skill is the method those hands follow. It only works when the Capacities MCP connector is active in this client.

## Configuration (edit once, then leave it)

These are David's real type and property keys, confirmed against the live space with `getObjectTypeShape`. The frontmatter write uses the exact keys below, not the display labels. Get a key wrong and the link silently drops into the body as plain text.

- **Target object type:** `Idea`
- **Entity-link property keys on that type** (all expect `[[Linked Object Title]]` wiki-link values referencing the object by its exact title, not an ID):
  - `initiatives` (links to the `Initiative` type; current objects: Local Community, Mentoring, CFPA, EXELA)
  - `relatedIdeas` (links to other `Idea` objects, self-referencing)
  - `people` (links to the `Person` type)
- **Tags:** the `tags` key links to the tag type. Apply from David's existing tags only, for example governance, ai-skills, pricing, partnerships. Never invent a tag that does not already exist.
- **Status tag:** default to `open` unless the chat clearly resolves the matter, in which case use `actioned`.
- **Source link:** there is no Source property, so put the chat link as a plain inline markdown link at the top of the body.

If the shape ever changes, re-run `getObjectTypeShape` on `Idea` and trust the live keys over this list.

## The workflow

Run these steps in order. Do not skip the search or the verification.

### 1. Write the summary first

Produce a self-sufficient summary of the conversation. The link will rot and the chat can be deleted, so the note must stand alone if the link dies. Structure it under three headings:

- **Decisions reached** — what was settled.
- **Open threads** — what is unresolved or deferred.
- **Considered and rejected** — paths looked at and dropped, with the reason. This is the part future David actually needs, so do not quietly omit it the way a flattering recap would.

Write the summary in David's voice. British English, no em dashes, no AI-tell vocabulary, no throat-clearing openers or closing pleasantries. If the `text-dna` skill is available, apply it. Keep it tight: this is a record, not an essay.

### 2. Find the connections (read step)

Call the connector `search` tool with the key nouns from the summary: the initiative, the people, the themes, any distinctive object names. Search is keyword plus semantic, so it finds related notes by meaning, not just exact title.

Capture the **exact title** of each genuine match, because the links are written as `[[Title]]` wiki-links and must match the object's real title precisely. Do not guess or fabricate a title. If search returns nothing relevant for a given property, leave that property empty rather than forcing a link.

Search is best-effort and ranked, not exhaustive, so it surfaces the obvious neighbours rather than every possible one. That is fine. The user verifies at the end.

### 3. Read the type shape (read step)

Call `getObjectTypeShape` on `Idea` to confirm the property keys are still `initiatives`, `relatedIdeas` and `people`, and still expect `[[Title]]` values. They were correct at setup, but a rename in Capacities would change them. This is the cheap check that stops a write from silently dropping links into the body. If the shape matches the Configuration block, proceed; if it has drifted, follow the live shape and tell David the config needs updating.

### 4. Create the object (write step)

Call `createObjectViaMd` against the `Idea` type. Put the links in the frontmatter using the exact property keys (`initiatives`, `relatedIdeas`, `people`), and write each value as a `[[Title]]` wiki-link referencing the object by its exact title from step 2, not an ID. Put the summary in the markdown body, with the chat link as a plain inline markdown link at the top.

A distinction that matters: the `[[Title]]` format belongs in the frontmatter property values, where it is the documented way to create the link. Do not scatter `[[ ]]` wiki-links through the body prose expecting them to resolve into backlinks; that is not reliable. The real links come from the frontmatter keys, so that is the only place they go.

Frontmatter shape (keys are fixed; titles come from your search matches):

```markdown
---
title: <short descriptive title, not the whole first line>
initiatives: [[CFPA]]
relatedIdeas: ["[[Some related idea]]", "[[Another idea]]"]
people: ["[[Jane Smith]]"]
---

[link back to chat](<chat URL>)

## Decisions reached
...

## Open threads
...

## Considered and rejected
...
```

Use a single `[[Title]]` for one match and a list for several. Omit a key entirely if there was no match for it. After creating, apply the theme and status tags.

### 5. Verify and report

Call `createObjectLink` to get a URL to the new object and give it to David so he can open it. Tell him plainly:

- the title and type created
- which objects it was linked to (initiatives, relatedIdeas, people)
- which links you could not make because no match was found
- the tags applied

Keep the report to a few lines. If any link failed to land, say so rather than implying everything wired up cleanly.

## Edge cases

- **No related objects found.** Create the note unlinked, set `initiatives` if David named one in the chat, and flag that it went in without graph links so he can connect it by hand.
- **Connector not active.** Stop and tell him the Capacities connector needs to be connected in this client first. Do not pretend to write.
- **Wrong initiative ambiguous.** If two initiatives could fit and the chat does not make it obvious, ask once rather than guessing. A wrong link is worse than a missing one.
- **Multiple distinct topics in one chat.** The connector works best one object at a time. Offer to create separate Idea objects rather than cramming unrelated threads into one note.
- **Counting or sweeping requests.** "Pull every Idea tagged CCC and summarise" is not supported by the connector and will return partial results. Say so; do not present a partial sweep as complete.

## What this skill will not do

It does not add capability the connector lacks. It will not make wiki-links resolve, will not traverse the whole graph, and will not batch-rewire existing notes. It makes one good capture repeatable and hands-free. That is the whole job.
