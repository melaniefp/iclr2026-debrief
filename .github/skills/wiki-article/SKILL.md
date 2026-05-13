---
name: wiki-article
description: Write a longer-form wiki article synthesizing multiple sources. Use this skill when asked to write an article, overview, or deep-dive on a topic.
---

# Wiki Article

This skill creates longer-form wiki articles that synthesize multiple sources from `raw/`, `wiki/papers/`, and existing `wiki/` content into cohesive narratives.

## When to use this skill

- User asks to "write an article about X"
- User asks for a "deep dive", "overview", or "synthesis" of a topic
- User wants to combine insights from multiple papers or raw captures into a single document

## Step 1: Understand the topic

Clarify with the user:

1. What topic or question the article should address
2. What scope — broad overview vs. focused analysis
3. Any specific sources they want included

## Step 2: Gather sources

Search the knowledge base for relevant material:

1. **`wiki/papers/`**: Search frontmatter (title, keywords, category) and content for related papers
2. **`raw/`**: Search frontmatter (title, tags) and content for related captures
3. **`wiki/concepts/`**: Find existing concept pages on the topic
4. **`wiki/summaries/`**: Find existing summaries of relevant sources

List all found sources and confirm with the user before proceeding. The user may want to add or exclude specific sources.

## Step 3: Read and analyze sources

For each source:

1. Read the full content
2. Extract the key claims, findings, or arguments relevant to the article topic
3. Note any contradictions or tensions between sources
4. Identify the narrative arc — how do these sources relate to each other?

## Step 4: Write the article

Create the article at `wiki/articles/<topic-slug>.md`:

```yaml
---
title: "Article Title"
type: article
tags:
  - tag1
  - tag2
related:
  - "wiki/concepts/concept-1.md"
  - "wiki/concepts/concept-2.md"
sources:
  - "raw/source-1.md"
  - "wiki/papers/paper-1.md"
---
```

### Article structure

```markdown
# Article Title

## TL;DR

{One paragraph summary of the article's main argument or findings}

## Introduction

{Set up the problem or topic. Why does this matter? What's the current state of the field?}

## {Main sections}

{Organize by theme, chronology, or argument structure — whatever fits best.
Use standard markdown links to reference concepts, papers, and raw captures throughout.
Include inline citations like "According to [paper-name](../papers/paper-name.md), ..." or "As discussed in [blog-post](../../raw/blog-post.md), ..."}

## Key takeaways

{Numbered list of the most important points}

## Open questions

{What remains unknown or debated? What would be interesting to explore next?}

## Sources

{Bulleted list of all sources used, with brief annotations}
- [papers/paper-name](../papers/paper-name.md) — {what this paper contributed to the article}
- [raw/blog-post](../../raw/blog-post.md) — {what this capture contributed}
```

### Writing guidelines

- **Voice**: Analytical and accessible. Write for a researcher who knows ML but may not know this specific sub-area.
- **Citations**: Use standard markdown links inline when referencing specific claims from sources. Every factual claim should be traceable to a source.
- **Math**: Use LaTeX (`$...$` for inline, `$$...$$` for display). No Unicode math symbols.
- **Figures**: If you reference figures from papers, link to the arxiv HTML version where possible.
- **Length**: Aim for 1000–3000 words depending on topic complexity.
- **Objectivity**: Present multiple viewpoints when sources disagree. Note limitations and caveats.

## Step 5: Update backlinks and index

After creating the article:

1. For each source referenced in the article, check its `related` frontmatter and add a backlink to the article if missing
2. For each concept referenced, add the article to the concept's `related` list
3. Update `wiki/README.md` to include the new article in the Articles section

## Step 6: Report completion

Provide a summary:

```
📄 Article created: wiki/articles/<slug>.md
- Title: <title>
- Sources used: N papers, N raw captures, N concepts
- Word count: ~N words
- New backlinks added: N

Suggested next steps:
- Review and refine the article
- Create any missing concept pages mentioned in the article
- Run wiki-update to ensure full consistency
```
