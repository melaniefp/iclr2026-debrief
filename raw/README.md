# Raw Captures

Markdown files converted from web content (blog posts, OpenReview discussions, social media threads) and source-file captures (LaTeX, Typst, slides, figures). This folder is **append-mostly** — files are rarely edited after creation.

## Conventions

### Web captures (single files)

- One file per captured URL: `raw/<slug>.md`
- Slugs are lowercase, hyphenated, derived from the title (e.g., `scaling-laws-for-neural-lms.md`)
- Every file **must** have YAML frontmatter (see schema below)
- Use standard markdown links (`[text](path)`) for cross-references to wiki concepts and paper summaries
- Preserve the original content structure (headings, code blocks, images) as faithfully as possible

### Source captures (folders)

- One folder per artifact: `raw/<slug>/` (slug typically ends in `-src`)
- Every folder **must** contain a `README.md` with YAML frontmatter
- Multi-file artifacts (LaTeX projects, slide decks with figures, etc.) are stored together
- Use the **`web-capture`** skill for the full workflow

## Frontmatter schema

```yaml
---
title: "Article title"
url: "https://..."
source: "blog | openreview | twitter | reddit | other"
author: "Author name"
date: "YYYY-MM-DD"           # Original publication date
captured: "YYYY-MM-DD"       # Date this file was created
tags:
  - tag1
  - tag2
aliases:
  - "alternative name"
related:
  - "wiki/concepts/some-concept.md"
  - "wiki/papers/some-paper-title.md"
---
```

### Field reference

| Field      | Required | Description                                      |
|------------|----------|--------------------------------------------------|
| `title`    | ✅       | Title of the source                               |
| `url`      | ✅       | Original URL                                      |
| `source`   | ✅       | One of: `blog`, `openreview`, `twitter`, `reddit`, `other` |
| `author`   | ✅       | Author or handle                                  |
| `date`     | ✅       | Original publication date (`YYYY-MM-DD`)          |
| `captured` | ✅       | Capture date (`YYYY-MM-DD`)                       |
| `tags`     | ✅       | List of topic tags for indexing                   |
| `aliases`  |          | Alternative names for this source                 |
| `related`  |          | Links to related wiki concepts or papers          |

## Creating new captures

Use the **`web-capture`** skill for all capture types:
> "Capture this URL into raw/: https://example.com/article"
> "Capture the LaTeX sources for arxiv paper 2401.12345"
> "Capture the oral presentation for this talk: https://..."
> "Store these slides in raw/"
