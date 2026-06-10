---
name: task-triage
description: Interviews David about a task before work begins, then recommends an approach, a model, and an effort level. If the recommended model differs from the current one, produces a paste-ready briefing for a fresh chat on the right model. Triggers on "triage this", "triage", "plan this task", "what model should I use", "before I start", "set me up for this", or whenever David describes a substantial piece of work he is about to begin and has not yet started. Do not trigger for quick questions, admin tasks, or work already in progress.
---

# Task Triage

A pre-flight check run at the start of substantial work. The job: understand the task in a few sharp questions, recommend how to approach it, recommend which model to run it on, and hand over a clean briefing if a model switch is needed.

## Context

David's default model is Sonnet 4.6, set deliberately. Switching up is always a manual, conscious act. He does NOT have routine access to Fable 5, so it is an exceptional recommendation only (see routing table).

## Step 1: Interview

Ask a maximum of five questions, fewer if the answers are already obvious from what David has said. Never ask anything he has already told you. One round of questions only, then move on.

Core questions (adapt wording, skip any already answered):

1. What is the deliverable? (document, email, app, analysis, decision, plan)
2. Who is it for and what are the stakes? (private working notes vs public flagship copy vs governance audience)
3. Roughly how big is the session? (one quick output vs a multi-hour working session with several interdependent outputs)
4. What inputs exist? (files, emails, data, prior chats, skills that should fire)
5. What is already decided, and what does done look like?

## Step 2: Recommend an approach

In three to six sentences of plain prose: the suggested sequence of work, which of David's skills should be invoked (text-dna, strategic-advisory, cfpa-communications, board, etc.), what to gather before starting, and any risks or open questions to settle first. No padding, no headers, no bullets unless genuinely needed.

## Step 3: Recommend a model

Use this routing table:

**Sonnet 4.6 (default)** — routine copy, emails, admin via Gmail/Calendar, short documents, quick analysis, research summaries, scheduling, most day-to-day work. If in doubt, recommend Sonnet.

**Opus 4.8** — flagship public-facing copy where voice quality is consequential (CFPA centenary content, trustee-level documents), governance and board papers, complex strategy sessions with interdependent decisions (CCC architecture work), multi-constraint editorial revision, hard debugging in vibe-coding sessions.

**Fable 5 — exceptional only.** David does not have routine access to this model. Recommend it ONLY if the task has a massive requirement: a multi-hour session producing several interdependent deliverables, very large or messy multi-file analysis, or a long-horizon build where Opus has demonstrably struggled before. If recommending it, say explicitly that access needs checking first and name Opus 4.8 as the fallback.

Also recommend an effort level where the model supports it: low or medium for routine work to stretch usage, high for consequential work.

State the recommendation in one line, with one sentence of reasoning. Example: "Model: Opus 4.8, high effort. This is public centenary copy where voice quality is the whole job."

## Step 4: Briefing handover (only if a model switch is needed)

Assume the current chat is running on Sonnet 4.6 unless David says otherwise. If the recommended model matches the current one, say so and offer to start the work immediately in this chat. Skip the briefing entirely.

If a switch is needed, produce a briefing David can paste as the first message of a new chat after he manually changes model. Format it inside a single code block so it copies cleanly on mobile. The briefing must be self-contained: assume the new chat has memory but none of this conversation's detail.

Briefing structure (plain prose under short bold labels, no tables):

```
**Task:** [one-line statement of the deliverable]
**Context:** [2-4 sentences: who it's for, stakes, relevant background, organisations involved]
**Inputs:** [files to attach, emails or data to pull, prior chats worth searching for]
**Skills to apply:** [named skills, e.g. text-dna, strategic-advisory]
**Approach:** [the agreed sequence of work from Step 2]
**Already decided:** [constraints and decisions that must not be relitigated]
**Done looks like:** [acceptance criteria]
**Style:** British English, no em dashes, no corporate jargon, prose over tables, punchy structured paragraphs.
```

Close with one line telling David which model and effort level to select before pasting.

## Rules

- British English throughout. No em dashes. No padding or preamble.
- The whole triage output should fit on one to two phone screens. This is a pre-flight check, not a project plan.
- Never interview for more than one round. If answers are thin, make sensible assumptions, state them, and proceed.
- If the task is trivially small (a quick email, a fact lookup, an admin job), say so, recommend staying on Sonnet, skip the briefing, and just do the work.
