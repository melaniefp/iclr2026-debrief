---
name: wiki-update
description: Update the wiki with summaries, concepts, and backlinks after new content is added. Use this skill when asked to update or refresh the wiki, or after adding new content to raw/.
---

# Wiki Update

This skill maintains the wiki knowledge graph by scanning `raw/` for new content and ensuring summaries, concept pages, and backlinks are up to date.

## When to use this skill

- User asks to "update the wiki" or "refresh the wiki"
- User has just added new content to `raw/` and wants the wiki updated
- User asks to "create summaries" or "update backlinks"

## Step 1: Identify new or modified content

Scan `raw/` for files that don't yet have corresponding entries in the wiki:

1. List all files and folders in `raw/` (excluding README.md)
2. List all files in `wiki/summaries/`
3. List all files in `wiki/papers/` (paper summaries already created by the `paper-summary` skill)
4. Identify `raw/` entries that have no matching summary in `wiki/summaries/` **and** no corresponding paper summary in `wiki/papers/`

Report the findings to the user before proceeding.

## Step 2: Create summaries for new content

For each new `raw/` entry without a wiki summary (and not already covered by a paper summary in `wiki/papers/`):

1. Read the source file or folder README from `raw/`
2. Write a concise summary (3–5 paragraphs) capturing the key points
3. Extract key concepts mentioned in the source
4. Save to `wiki/summaries/<slug>.md` with frontmatter:

```yaml
---
title: "Summary: <source title>"
type: summary
tags:
  - tag1
  - tag2
related:
  - "wiki/concepts/concept-name.md"
sources:
  - "raw/source-slug.md"
---
```

The summary should:
- Start with a one-sentence TL;DR
- Highlight the main claims or contributions
- Note any connections to other content in the knowledge base
- Use standard markdown links (`[text](path)`) to reference concepts and other sources

## Step 3: Update or create concept pages

For each key concept found in the new content:

1. Check if `wiki/concepts/<concept-slug>.md` already exists
2. **If it exists**: add the new source to its `sources` list and update the content if the new source provides significant new information
3. **If it doesn't exist**: create a stub concept page:

```yaml
---
title: "Concept Name"
type: concept
tags:
  - tag1
related:
  - "wiki/concepts/other-concept.md"
sources:
  - "raw/source-slug.md"
  - "wiki/papers/paper-slug.md"
---
```

```markdown
# Concept Name

{Brief definition — 1–2 sentences}

## Key ideas

- {Bullet points summarizing the concept from available sources}

## Sources

- [source-slug](../../raw/source-slug.md) — {one-line note on what this source says about the concept}
- [paper-slug](../papers/paper-slug.md) — {one-line note}

## Related concepts

- [related-concept-1](related-concept-1.md)
- [related-concept-2](related-concept-2.md)
```

Concept names should be specific enough to be useful but general enough to aggregate multiple sources. For example, prefer "mixture-of-experts" over "mixture-of-experts-in-transformers".

## Step 4: Ensure bidirectional backlinks

For every cross-reference link in the wiki:

1. Check that the target file exists
2. Check that the target file links back to the source
3. If a backlink is missing, add it to the target's `related` or `sources` frontmatter

Also check `raw/` files — if a raw capture mentions a concept that now has a wiki page, add a `related` link in the raw file's frontmatter.

## Step 5: Update the wiki index

Update `wiki/README.md` to reflect the current state:

1. **Concepts section**: List all concept pages alphabetically with a one-line description
2. **Summaries section**: List all summaries grouped by source type (raw captures vs. papers)
3. **Articles section**: List all articles with a one-line description

Use this format:
```markdown
### Concepts

- [Concept Name](concepts/concept-slug.md) — Brief description

### Summaries

- [Summary Title](summaries/summary-slug.md) — Source: [raw/slug](../raw/slug.md) or [wiki/papers/slug](papers/slug.md)

### Articles

- [Article Title](articles/article-slug.md) — Brief description
```

## Step 6: Report changes

Provide a summary of all changes made:

```
📝 Wiki update complete:
- Created N new summaries
- Created N new concept stubs
- Updated N existing concept pages
- Fixed N missing backlinks
- Updated wiki/README.md index
```
