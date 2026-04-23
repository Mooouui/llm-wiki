---
title: "RAG"
type: concept
tags: [architecture, retrieval, knowledge-management]
sources: [llm-wiki-complete-guide]
last_updated: 2026-04-09
---

# RAG (Retrieval-Augmented Generation)

The dominant paradigm for LLM-powered knowledge access: split documents into chunks, embed them as vectors, store in a database, perform similarity search at query time, feed results to an LLM for answer generation.

## Fatal Flaw (per LLM Wiki critique)

RAG has **no accumulation**. Every complex query requires re-retrieval and re-synthesis. Knowledge does not grow with use. ChatGPT file uploads, NotebookLM, and most RAG systems offer a "read-once-and-forget" experience.

## LLM Wiki vs RAG

| Dimension | RAG | LLM Wiki |
|-----------|-----|----------|
| Processing timing | Query time (every time) | Ingest time (once per source) |
| Cross-referencing | Discovered per query | Pre-built and maintained |
| Contradiction detection | Often missed | Flagged at ingestion |
| Knowledge growth | None — starts from zero each time | Compound interest |
| Output format | Ephemeral chat replies | Persistent Markdown files |
| Human role | Upload files + ask questions | Curate sources, explore directions |

## Connections

- [[LLMWiki|LLM Wiki]] — the alternative paradigm
- [[NotebookLM]] — shares RAG's fundamental limitation
