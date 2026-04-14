---
type: entity
domain: pkm
tags: [tool, app, markdown, pkm, obsidian]
created: 2026-04-13
updated: 2026-04-13
sources: [defileo-claude-obsidian-second-brain]
---

# Obsidian

A local-first markdown note-taking application used as the vault layer in the [[llm-wiki-pattern]] setup.

---

## Overview

Obsidian is a desktop application for managing interconnected markdown files stored locally on disk. Notes live as plain `.md` files in a folder called a "vault," making them fully portable, version-controllable with git, and accessible by any tool that can read files — including LLMs. Its graph view visualises connections between notes; its plugin ecosystem (Dataview, Marp, Web Clipper) extends its capabilities significantly.

---

## Key Facts

| Attribute | Value |
|-----------|-------|
| Type | Desktop application (Mac, Windows, Linux, iOS, Android) |
| File format | Plain markdown (.md) |
| Storage | Local-first (optional sync) |
| Notable plugins | Dataview, Marp, Obsidian Web Clipper |

---

## What the Wiki Knows

In the [[llm-wiki-pattern]] context, Obsidian's role is as the **UI layer** — it is where the human reads and navigates the wiki that the LLM writes. As [[defileo]] notes, Obsidian is technically optional: the LLM can maintain the vault entirely from the terminal, and Obsidian is "just the window you look through when you want to see what's inside." Its graph view is particularly useful for spotting orphan pages and understanding the shape of the knowledge base.

Useful Obsidian features for this setup:
- **Web Clipper** (browser extension): converts web articles to markdown and saves them to a configured folder in the vault — the primary ingestion mechanism for web sources.
- **Attachment folder setting:** can be configured to save images to `raw/assets/` automatically.
- **Dataview plugin:** runs queries over YAML frontmatter — useful for dynamic indexes and dashboards if pages have consistent frontmatter.
- **Graph view:** best way to see hub pages, orphans, and cluster structure at a glance.

---

## Appearances in Sources

- [[defileo-claude-obsidian-second-brain]] — central tool in the setup; described as the vault/UI layer

---

## Related Entities & Concepts

- [[claude-code]] — the LLM agent that writes and maintains the vault Obsidian displays
- [[obsidian-web-clipper]] — the browser extension for clipping sources into the vault
- [[llm-wiki-pattern]] — the architecture Obsidian is used within
- [[second-brain]] — the PKM concept Obsidian is used to implement
