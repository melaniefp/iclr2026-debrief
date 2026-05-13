# Copilot Instructions

## Project overview

Knowledge base for ICLR 2026 research. The repo organizes raw captures and curated wiki content into a cross-linked knowledge graph:

- **`raw/`** — Markdown captures from web content (blog posts, OpenReview discussions, social media threads) with YAML frontmatter, and source-file captures (LaTeX, Typst, slides, figures) stored as folders. Append-mostly; rarely edited after creation.
- **`wiki/`** — Curated knowledge base with paper summaries, concept definitions, short summaries of raw captures, topic overviews, and longer-form synthesis articles. Cross-links to `raw/` sources.

## Folder structure

```
raw/                    # Web captures and source-file captures
  README.md             # Conventions & frontmatter schema
  <slug>.md             # One file per captured URL (web captures)
  <slug>/               # Folder per multi-file artifact (source captures)
    README.md           # Metadata for the artifact
    *.tex, *.typ, etc.  # Source files

wiki/                   # Curated knowledge base
  README.md             # Index of all wiki content
  papers/               # Paper summaries (from paper-summary skill)
  concepts/             # Concept articles (e.g., mixture-of-experts.md)
  summaries/            # Short summaries of raw/ entries
  articles/             # Longer-form synthesis articles
```

## Frontmatter conventions

All markdown content files use YAML frontmatter. Schemas are defined in the README of each folder.

### raw/ files

```yaml
---
title: "Article title"
url: "https://..."
source: "blog | openreview | twitter | reddit | other"
author: "Author name"
date: "YYYY-MM-DD"
captured: "YYYY-MM-DD"
tags: [tag1, tag2]
aliases: ["alternative name"]
related: ["[concept](wiki/concepts/concept.md)", "[paper-title](wiki/papers/paper-title.md)"]
---
```

### wiki/ files

```yaml
---
title: "Page title"
type: "concept | summary | article"
tags: [tag1, tag2]
related: ["[linked-page](../concepts/linked-page.md)"]
sources: ["[raw/slug](../../raw/slug.md)", "[wiki/papers/slug](../papers/slug.md)"]
---
```

### wiki/papers/ files

```yaml
---
title: "Paper title"
authors: "Authors"
affiliations: "Affiliations"
url: "https://..."
date: "YYYY-MM-DD"
category: "Category"
keywords: [kw1, kw2, kw3]
---
```

## Cross-referencing

Use standard markdown links for all cross-references. Paths are relative to the file's location:

- `[Concept Name](../wiki/concepts/concept-name.md)` — from a raw/ file to a wiki concept
- `[Source Title](../../raw/slug.md)` — from a wiki file to a raw capture
- `[Paper Title](../papers/paper-slug.md)` — from a wiki file to a paper summary

In YAML frontmatter `related` and `sources` fields, use repo-root-relative paths for consistency:

- `wiki/concepts/concept-name.md`
- `raw/slug.md`
- `wiki/papers/paper-slug.md`

Backlinks should be bidirectional: if A links to B, B should link back to A.

## Workflow

The typical workflow for adding knowledge to the base:

1. **Capture** — Use `web-capture` skill to save content to `raw/` (web pages, source files, oral transcripts, slides), or `paper-summary` skill to download sources to `raw/` and create a summary in `wiki/papers/`
2. **Summarize** — Use `wiki-update` skill to create wiki summaries and concept stubs for new content
3. **Synthesize** — Use `wiki-article` skill to write longer-form articles combining multiple sources

## Skills

| Skill              | When to use                                                   |
|--------------------|---------------------------------------------------------------|
| `web-capture`      | Capture any content into `raw/` — web pages, source files, orals, slides |
| `wiki-update`      | Update wiki after adding new content (summaries, backlinks)   |
| `wiki-article`     | Write a synthesis article combining multiple sources          |
| `paper-summary`    | Summarize a research paper (sources → `raw/`, summary → `wiki/papers/`) |
| `commit`           | Safely commit changes with pre-commit checks                  |

## Git workflow

- **Do not commit unless explicitly asked**. After completing a task, summarize what was done and let the user decide when to commit.
- **Branch naming**: `copilot/<descriptive-name>` for Copilot-created branches.
- **Commit messages**: Conventional commits — `type(scope): description`. Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `ci`.
- **Selective staging only**: Never run `git add .` or `git add -u`. Stage individual files with `git add <file>`.
- **Pre-commit hooks** run automatically on commit (codespell, trailing-whitespace, end-of-file-fixer, check-json5, check-ast, etc.). If hooks auto-fix files, re-stage and re-commit.
- **Codespell false positives**: Add terms to `ignore-words-list` in `.codespellrc` rather than changing legitimate technical terms.
