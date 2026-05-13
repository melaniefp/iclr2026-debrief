# :sparkles: iclr2026

[![main](https://github.com/msr-cambridge-uk/iclr2026/actions/workflows/main.yml/badge.svg)](https://github.com/msr-cambridge-uk/iclr2026/actions/workflows/main.yml)
[![Checked with pyright](https://microsoft.github.io/pyright/img/pyright_badge.svg)](https://msr-cambridge-uk.github.io/pyright/)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Knowledge base for ICLR 2026 research — raw captures and a curated wiki organized into a cross-linked knowledge graph.

## Structure

| Folder     | Purpose                                                        |
|------------|----------------------------------------------------------------|
| `raw/`     | Markdown captures from blogs, OpenReview, social media, source files, and oral transcripts |
| `wiki/`    | Curated knowledge base: paper summaries, concepts, topic overviews, and synthesis articles  |

All content is cross-linked using standard markdown links.

## Quick start

### Capture content

> "Use the web-capture skill to capture this URL: https://..."
> "Use the web-capture skill to capture the LaTeX sources for arxiv paper 2401.12345"
> "Use the web-capture skill to capture the oral for this talk: https://..."

Saves web pages as markdown files, or source files / oral transcripts as folders in `raw/`.

### Summarize a paper

> "Use the paper-summary skill to summarize this paper: https://arxiv.org/abs/..."

Creates a structured summary in `wiki/papers/` with contributions, findings, and implementation notes.

### Update the wiki

> "Use the wiki-update skill to update the wiki"

Scans for new content in `raw/`, creates summaries, stubs concept pages, and maintains backlinks.

### Write a synthesis article

> "Use the wiki-article skill to write an article about mixture-of-experts"

Synthesizes multiple sources into a longer-form article in `wiki/articles/`.
