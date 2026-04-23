---
title: "Schema"
type: concept
tags: [architecture, configuration, llm-agent]
sources: [llm-wiki-complete-guide]
last_updated: 2026-04-09
---

# Schema (Control Protocol Layer)

A configuration document that tells the LLM agent how to maintain the wiki. The "switch" that turns a generic chatbot into a strict "knowledge librarian." Without it, every new session starts from zero.

## Examples by Agent

| Agent | Schema File |
|-------|------------|
| Claude Code | `CLAUDE.md` |
| Codex | `AGENTS.md` |
| Gemini CLI | `GEMINI.md` |

## What It Defines

- Directory structure and access rules
- Page format (frontmatter fields, tags, wikilink conventions)
- Ingestion workflow (step-by-step)
- Query workflow
- Lint/health-check workflow
- Naming conventions

## Evolution

The schema is co-evolved between human and LLM. As you use the wiki, you discover what page structures work, which frontmatter fields are valuable, and which workflows need adjustment — then update the schema accordingly.

## Connections

- [[LLMWiki|LLM Wiki]] — the control layer for the system
- [[ClaudeCode|Claude Code]] — reads CLAUDE.md as its schema