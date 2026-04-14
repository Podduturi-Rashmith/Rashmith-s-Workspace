---
type: concept
domain: pkm
tags: [llm, wiki, knowledge-management, architecture, pattern]
created: 2026-04-13
updated: 2026-04-13
sources: [defileo-claude-obsidian-second-brain]
---

# LLM Wiki Pattern

An architecture for personal knowledge management in which an LLM incrementally builds and maintains a persistent, interlinked markdown wiki over a collection of raw source documents — rather than rediscovering knowledge from scratch at query time.

---

## Explanation

The LLM Wiki pattern has three layers:

1. **Raw sources** — immutable source documents (articles, PDFs, transcripts). The LLM reads these but never modifies them.
2. **The wiki** — a directory of LLM-generated markdown files: summaries, entity pages, concept pages, a synthesis overview, an index, and a log. The LLM owns this layer entirely.
3. **The schema** — a configuration document (e.g. `CLAUDE.md`) that tells the LLM the directory structure, naming conventions, page formats, and step-by-step workflows for ingesting sources, answering queries, and maintaining the wiki.

When a new source is added, the LLM reads it, extracts key information, writes a summary page, and updates all related entity and concept pages across the wiki — potentially touching 10–15 files per source. Crucially, knowledge is *compiled once and kept current*, not re-derived on every query.

---

## Why It Matters

The bottleneck in personal knowledge management is not reading or thinking — it's bookkeeping: keeping cross-references current, updating summaries when new sources arrive, noting contradictions, maintaining consistency. This burden causes most wikis and second-brain systems to decay. LLMs eliminate this cost because they don't get bored, don't forget to update a cross-reference, and can touch many files in one pass. The wiki compounds indefinitely.

The pattern is the modern realisation of [[vannevar-bush]]'s [[memex]] vision: a private, curated knowledge store where connections between documents are as valuable as the documents themselves. Bush couldn't solve the maintenance problem. The LLM handles it.

---

## Three Core Operations

| Operation | Trigger | What happens |
|-----------|---------|--------------|
| **Ingest** | New source dropped in `raw/` | LLM reads, summarises, creates/updates 10–15 wiki pages, logs changes |
| **Query** | User asks a question | LLM reads index → relevant pages → synthesises answer with citations; optionally files the answer |
| **Lint** | Periodic health check | LLM scans for orphans, contradictions, stale claims, missing pages; produces a fix checklist |

---

## How Sources Treat This Concept

[[defileo-claude-obsidian-second-brain]] presents the LLM Wiki pattern as the operating architecture behind a Claude + Obsidian "second brain." Leo implements it via copy-paste CLI prompts and frames it as the solution to the chronic failure mode of PKM systems. He credits [[andrej-karpathy]] as the originator.

The schema governing this vault (`CLAUDE.md`) is a direct implementation of Karpathy's pattern, instantiated for a general-purpose personal vault covering research, books, projects, competitive analysis, and more.

---

## Related Concepts

- [[second-brain]] — the PKM framing this pattern is often used to implement
- [[rag]] — the alternative approach this pattern contrasts with
- [[morning-digest-automation]] — an automation pattern that extends the core workflow
- [[memex]] — the 1945 conceptual ancestor

---

## Related Entities

- [[andrej-karpathy]] — originator
- [[defileo]] — practitioner who popularised it
- [[claude-code]] — the LLM agent that executes the pattern in this vault
- [[obsidian]] — the UI layer used to navigate the wiki

---

## Appearances in Sources

- [[defileo-claude-obsidian-second-brain]] — the thread that introduced this concept to this wiki; Leo's implementation guide

---

## Open Questions

- At what vault size (number of pages, number of sources) does the `index.md` approach break down and require a proper search tool like `qmd`?
- How should the `Memory.md` pattern (user context file) be structured for maximum effectiveness?
- What is the optimal cadence for lint passes as the vault grows?
