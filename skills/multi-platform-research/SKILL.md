---
name: multi-platform-research
description: "Conducts a comprehensive 30-day research brief across the web, news, Reddit, Hacker News, and social platforms. Triggers on: 'research [topic]', 'last 30 days on [topic]', 'what is the word on [topic]', 'what are people saying about [topic]', 'find me info on [topic]', 'run research on [topic]', or any variation where the goal is a multi-source research brief. Also use for competitor research, trend discovery, tool comparisons, and audience sentiment analysis."
---

# Multi-Platform Research

Multi-source research agent that synthesises what people are actually saying about a topic across the web, Reddit, Hacker News, and social platforms — all within the past 30 days.

## Invoking the skill

The user will provide a topic. If no topic is specified, ask for one before proceeding.

## Workflow

Run Phases 1–3 in parallel where possible, then synthesise.

### Phase 1: Reddit

Fetch Reddit's public search JSON API — no API key needed:

```
https://www.reddit.com/search.json?q=TOPIC&sort=top&t=month&limit=25
https://www.reddit.com/search.json?q=TOPIC&sort=new&t=month&limit=15
```

From each result, extract: post title, subreddit, score, number of comments, date, URL.

For the top 3–5 posts by score, fetch the comment thread:
```
https://www.reddit.com/r/SUBREDDIT/comments/POST_ID.json?sort=top&limit=10
```

Look for recurring themes, complaints, praise, and questions in the comments.

### Phase 2: Hacker News

Fetch the Algolia HN search API:

```
https://hn.algolia.com/api/v1/search?query=TOPIC&tags=story&numericFilters=created_at_i>TIMESTAMP&hitsPerPage=20
https://hn.algolia.com/api/v1/search?query=TOPIC&tags=comment&numericFilters=created_at_i>TIMESTAMP&hitsPerPage=15
```

Calculate TIMESTAMP as Unix epoch for 30 days ago.

Extract: story title, URL, points, comment count, author, date, notable comment excerpts.

### Phase 3: Web Search

Run 2–3 targeted queries to catch recent news, reviews, and analysis:

- `"[TOPIC]" news` — for recent coverage
- `[TOPIC] review [current year]` — for honest evaluations
- `[TOPIC] problems OR complaints OR "worth it"` — for real opinions

For the 3–4 most relevant results, fetch actual page content — not just headlines.

### Phase 4: Synthesis

Combine all sources into a coherent briefing. Look for:

- **Consensus**: What do people broadly agree on across platforms?
- **Controversy**: Where is there real disagreement or debate?
- **Pain points**: What frustrations keep surfacing?
- **Excitement**: What are people genuinely enthusiastic about?
- **Emerging patterns**: What is new or gaining momentum vs settled wisdom?
- **Gaps**: What questions are not being answered well anywhere?

Cross-platform convergence is the strongest signal. If something shows up on Reddit AND HN AND the web, that is real.

## Output Format

Present the report directly in the chat using this structure:

- **Executive Summary**: Three sentences max.
- **Platform Breakdown**: Bulleted insights from each source.
- **Actionable Takeaway**: A "So What?" section for the user.

## Principles

- **No Hallucinations**: If search results are sparse, state that the topic has had low engagement in the last 30 days.
- **Citation Required**: Every claim must include a source link from the search results.
- **Human Voice**: Be direct and slightly critical if the sentiment is negative.
