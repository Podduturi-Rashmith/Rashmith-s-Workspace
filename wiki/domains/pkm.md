---
type: domain
domain: pkm
tags: [pkm, knowledge-management, second-brain, llm, obsidian]
created: 2026-04-13
updated: 2026-04-13
---
	
# PKM (Personal Knowledge Management)

Domain covering tools, systems, and patterns for capturing, organising, and compounding personal knowledge over time.

---

## Overview

This domain tracks everything related to how individuals build and maintain personal knowledge systems — from classical note-taking methods through to LLM-maintained wikis. The central theme emerging from current sources is the contrast between passive document storage (e.g. [[rag]]-based systems) and active, incrementally-maintained knowledge bases (the [[llm-wiki-pattern]]).

---

## Current Understanding

The dominant insight from sources ingested so far: **the failure mode of all PKM systems is maintenance decay**, not poor capture. People capture notes; they stop maintaining connections, summaries, and cross-references because it's tedious. The [[llm-wiki-pattern]] addresses this directly by delegating all bookkeeping to an LLM — making maintenance effectively free and the knowledge base self-sustaining.

The historical anchor is [[vannevar-bush]]'s [[memex]] (1945) — a vision of personal, associatively-linked knowledge stores. The LLM wiki is the first practical implementation of that vision at personal scale.

---

## Key Entities in This Domain

- [[obsidian]] — markdown vault application; UI layer for the wiki
- [[claude-code]] — LLM agent; writer and maintainer of the wiki
- [[obsidian-web-clipper]] — browser extension for source ingestion
- [[andrej-karpathy]] — originator of the LLM Wiki pattern
- [[defileo]] — practitioner who popularised the pattern
- [[vannevar-bush]] — historical figure; Memex creator

---

## Key Concepts in This Domain

- [[llm-wiki-pattern]] — the core architecture: raw sources + LLM-owned wiki + schema
- [[second-brain]] — the PKM framing most sources use
- [[rag]] — the contrasting approach: retrieval at query time vs. compiled wiki
- [[memex]] — 1945 conceptual ancestor
- [[morning-digest-automation]] — automation pattern extending the core workflow

---

## Sources in This Domain

| Source | Date | Contribution |
|--------|------|--------------|
| [[defileo-claude-obsidian-second-brain]] | 2026-04-08 | Practical setup guide for Claude + Obsidian second brain; popularisation of the LLM Wiki pattern; CLI prompts for ingest, lint, and morning digest |

---

## Open Questions & Gaps

- How does the `Memory.md` pattern work in detail? Worth seeking a dedicated source.
- Are there sources on the Karpathy LLM Wiki document directly (not via Leo's thread)?
- What does Tiago Forte's original "Building a Second Brain" say, and how does it compare to the LLM-native approach?
- At what scale does `index.md`-based navigation need to be replaced with vector search?
