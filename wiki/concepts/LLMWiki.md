---
title: "LLM Wiki"
type: concept
tags: [pattern, knowledge-management, llm, architecture]
sources: [llm-wiki-complete-guide]
last_updated: 2026-04-09
---

# LLM Wiki

A pattern (not a product) for personal/team knowledge management where an LLM agent continuously builds and maintains a structured, interlinked local Markdown knowledge base. Coined by [[Andrej Karpathy]] in April 2026.

## Core Principle

Process sources at **ingestion time**, not query time. Each source is "compiled" once into the wiki, then incrementally maintained. Knowledge compounds rather than being re-derived on every query.

## Three-Layer Architecture

| Layer | Directory | Mutability | Owner |
|-------|-----------|-----------|-------|
| Raw Sources | `raw/` | Immutable (LLM read-only) | Human |
| The Wiki | `wiki/` | Fully mutable | LLM |
| The Schema | `CLAUDE.md` / `AGENTS.md` | Evolving | Human + LLM |

## Three Core Operations

1. **Ingest** — Add a source to raw/, LLM reads it, creates source summary, updates entity/concept pages, builds cross-links, appends to log
2. **Query** — Ask a question, LLM searches wiki pages, synthesizes answer with [[wikilinks]], optionally archives the answer as a new synthesis page
3. **Lint** — LLM audits the wiki for orphans, broken links, contradictions, stale summaries, missing entity pages, and data gaps

## Key Index Files

- `wiki/index.md` — Spatial dimension: global catalog of all pages
- `wiki/log.md` — Temporal dimension: append-only activity log

These two plain-text files replace vector databases at small-to-medium scale (~100 sources, hundreds of pages).

## The Compounding Loop

Source ingested → Wiki updated → Query produces insight → Best insights archived as new pages → Wiki grows from both external sources and internal exploration.

## Connections

- [[RAG]] — the approach LLM Wiki superseded
- [[Zettelkasten]] — historical predecessor with key differences
- [[Memex]] — 1945 ancestor vision
- [[Schema]] — the control protocol layer
- [[Obsidian]] — recommended frontend
- [[Claude Code]] — recommended LLM agent
- [[Andrej Karpathy]] — originator
- [[NotebookLM]] — product contrast
- [[Hormesis]] — critical concern about cognitive friction
