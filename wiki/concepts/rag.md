---
type: concept
domain: pkm
tags: [ai, rag, retrieval, llm, knowledge-management]
created: 2026-04-13
updated: 2026-04-13
sources: [defileo-claude-obsidian-second-brain]
---

# RAG (Retrieval-Augmented Generation)

An approach to LLM-based question answering in which relevant document chunks are retrieved at query time and fed to the LLM as context — contrasted in this wiki with the [[llm-wiki-pattern]]'s approach of pre-compiling knowledge into a persistent wiki.

---

## Explanation

In a RAG system, a collection of source documents is chunked and embedded into a vector database. At query time, the user's question is embedded, semantically similar chunks are retrieved, and those chunks are injected into the LLM's context window alongside the question. The LLM then generates an answer grounded in those retrieved chunks. Tools like NotebookLM and ChatGPT file uploads operate on this principle.

---

## Why It Matters

RAG is the dominant paradigm for "chat with your documents" products. It scales to large document collections and requires no pre-processing beyond indexing. However, it has a fundamental limitation: knowledge is re-derived from scratch on every query. There is no accumulation. Cross-document synthesis requires all relevant chunks to surface in a single retrieval pass, which is unreliable for subtle or multi-hop questions.

---

## How Sources Treat This Concept

[[defileo-claude-obsidian-second-brain]] (via [[andrej-karpathy]]'s embedded text) positions RAG as the approach the [[llm-wiki-pattern]] replaces. The key critique: "the LLM is rediscovering knowledge from scratch on every question — there's no accumulation." The LLM wiki pattern pre-compiles knowledge into a structured wiki that is kept current incrementally, so synthesis, cross-references, and contradiction flags are already present at query time rather than being reconstructed each time.

---

## Related Concepts

- [[llm-wiki-pattern]] — the alternative architecture that contrasts with RAG
- [[second-brain]] — the broader PKM category both approaches serve

---

## Appearances in Sources

- [[defileo-claude-obsidian-second-brain]] — contrasted with the LLM wiki approach as the inferior alternative for personal knowledge management

---

## Open Questions

- At what scale does the `index.md`-based navigation in the LLM wiki pattern break down and require RAG-like retrieval (e.g. via `qmd`)?
- Are there hybrid approaches that combine pre-compiled wiki pages with vector search over raw sources?
