---
title: "Overview"
type: synthesis
tags: []
sources: [llm-wiki-complete-guide]
last_updated: 2026-04-09
---

# Overview

*This page is maintained by the LLM. It is updated on every ingest to reflect the current synthesis across all sources.*

## What is LLM Wiki?

LLM Wiki is a pattern (not a product) proposed by [[Andrej Karpathy]] in April 2026 for building personal knowledge bases where an LLM agent continuously writes, links, and maintains structured Markdown files. It inverts the traditional [[RAG]] paradigm: instead of re-processing sources on every query, sources are "compiled" once at ingestion time into a persistent, compounding wiki.

## The Architecture

Three layers of pure text — no vector databases needed at small-to-medium scale:

1. **Raw Sources** (`raw/`) — immutable originals; LLM reads but never modifies
2. **The Wiki** (`wiki/`) — LLM-generated and maintained; humans read, LLM writes
3. **The Schema** (`CLAUDE.md`) — control protocol defining how the LLM maintains the wiki

Two index files (`index.md` for spatial navigation, `log.md` for temporal tracking) serve as the navigation backbone.

## Core Operations

- **Ingest**: Add a source → LLM creates summary, updates entities/concepts, builds cross-links
- **Query**: Ask a question → LLM searches wiki, synthesizes with citations, optionally archives answer
- **Lint**: Health check → detect orphans, broken links, contradictions, stale content, gaps

## Key Tension: Automation vs. Understanding

The deepest critique comes from [[Extended Brain]], drawing on [[Niklas Luhmann]]'s [[Zettelkasten]] and the concept of [[Hormesis|cognitive friction]]. The argument: LLM Wiki produces excellent maps, but the user never walks the territory. The struggle of expressing ideas in your own words — when language breaks down and reveals understanding gaps — is not a bug but the mechanism of learning itself.

The recommended hybrid: use LLM for scaffolding (linking, indexing, gap-finding), but keep synthesis in your own hands.

## Historical Lineage

[[Vannevar Bush]]'s 1945 [[Memex]] envisioned a personal knowledge machine with associative trails. His unsolved problem — who does the maintenance? — is answered by LLMs. The web became public and chaotic; LLM Wiki returns to Bush's original vision of private, curated knowledge.
