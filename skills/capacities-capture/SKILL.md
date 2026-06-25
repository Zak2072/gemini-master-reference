---
name: capacities-capture
description: "Captures the current chat into Capacities as a properly linked object via the Capacities MCP connector. Searches the space for related objects first, then creates a typed note with its object-select properties populated so the result is genuinely wired into the graph, not just text. Use this whenever David says 'send this to Capacities', 'capture this', 'save this chat to Capacities', 'add this to my second brain', 'note this in Capacities', or otherwise wants a conversation, decision, or idea preserved in Capacities. Trigger even if he doesn't name the object type or the links explicitly, the skill handles that."
---

# Capacities Capture

Turn a chat into a single, well-linked object in David's Capacities space. The connector is the hands; this skill is the method those hands follow. It only works when the Capacities MCP connector is active in this client.

## Configuration (edit once, then leave it)

These are David's real type and property names. If they are wrong, he corrects them here and nowhere else.

- **Target object type:** `Idea`
- **Object-select properties on that type:**
  - `Initiative` (links to the `Initiative` type: EXELA, CFPA, CCC, Cheltenham Trust, Mentoring)
  - `Related Ideas` (links to other `Idea` objects)
  - `People` (links to the `Person` type)
- **Source property (optional):** `Source` (plain text or URL property for the chat link). If it does not exist, put the link inline in the body instead.
- **Theme tags:** apply from David's existing tags only, for example governance, ai-skills, pricing, partnerships. Never invent a tag that does not already exist.
- **Status tag:** default to `open` unless the chat clearly resolves the matter, in which case use `actioned`.

If the real names differ from the above, trust the live space over this list. Always confirm against `getObjectTypeShape` before writing.

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

Capture the object **ID and title** of each genuine match. These IDs are how the links get made. Do not guess or fabricate an ID. If search returns nothing relevant for a given property, leave that property empty rather than forcing a link.

Search is best-effort and ranked, not exhaustive, so it surfaces the obvious neighbours rather than every possible one. That is fine. The user verifies at the end.

### 3. Read the type shape (read step)

Call `getObjectTypeShape` on the target type (`Idea`) to get the exact property keys and the format each object-select property expects. Use whatever the shape tells you, not what this file assumes. This is the step that stops the write from silently dropping the links into the body as plain text.

### 4. Create the object (write step)

Call `createObjectViaMd`. Put the object-select links in the frontmatter, mapped to the property keys from step 3, referencing the objects found in step 2 by their ID (or by the format the shape requires). Put the summary in the markdown body. Put the chat link in the `Source` property if it exists, otherwise as a plain inline markdown link at the top of the body.

Do not write `[[ ]]` wiki-links in the body and assume they resolve into backlinks. Through the connector that is not reliable. Real links come from the frontmatter properties, so that is where they go.

Frontmatter shape (adapt keys to the live shape):

```markdown
---
title: <short descriptive title, not the whole first line>
Initiative: <matched Initiative object>
Related Ideas: [<matched Idea objects, if any>]
People: [<matched Person objects, if any>]
Source: <chat URL>
---

[link back to chat](<chat URL>)   <!-- only if no Source property exists -->

## Decisions reached
...

## Open threads
...

## Considered and rejected
...
```

After creating, apply the theme and status tags.

### 5. Verify and report

Call `createObjectLink` to get a URL to the new object and give it to David so he can open it. Tell him plainly:

- the title and type created
- which objects it was linked to (Initiative, Related Ideas, People)
- which links you could not make because no match was found
- the tags applied

Keep the report to a few lines. If any link failed to land, say so rather than implying everything wired up cleanly.

## Edge cases

- **No related objects found.** Create the note unlinked, set the Initiative if David named one in the chat, and flag that it went in without graph links so he can connect it by hand.
- **Connector not active.** Stop and tell him the Capacities connector needs to be connected in this client first. Do not pretend to write.
- **Wrong initiative ambiguous.** If two initiatives could fit and the chat does not make it obvious, ask once rather than guessing. A wrong link is worse than a missing one.
- **Multiple distinct topics in one chat.** The connector works best one object at a time. Offer to create separate Idea objects rather than cramming unrelated threads into one note.
- **Counting or sweeping requests.** "Pull every Idea tagged CCC and summarise" is not supported by the connector and will return partial results. Say so; do not present a partial sweep as complete.

## What this skill will not do

It does not add capability the connector lacks. It will not make wiki-links resolve, will not traverse the whole graph, and will not batch-rewire existing notes. It makes one good capture repeatable and hands-free. That is the whole job.
