---
type: entity
domain: pkm
tags: [tool, browser-extension, obsidian, ingestion]
created: 2026-04-13
updated: 2026-04-13
sources: [defileo-claude-obsidian-second-brain]
---

# Obsidian Web Clipper

A browser extension that converts web pages to markdown and saves them directly into an Obsidian vault — the primary ingestion mechanism for web-based sources.

---

## Overview

Obsidian Web Clipper is a browser extension (available for Chrome, Firefox, and others) maintained by the Obsidian team. When activated on a web page, it strips the page to its main content, converts it to clean markdown, and saves it to a configured folder inside an Obsidian vault. This makes it the natural first step in the [[llm-wiki-pattern]] ingest workflow: clip an article, and it lands in `raw/` ready for Claude to process.

---

## What the Wiki Knows

In the [[llm-wiki-pattern]] setup, Web Clipper handles the friction point between "reading something on the web" and "getting it into the vault." Without it, the user would have to manually copy, paste, and format web content. With it, saving an article to raw sources is a single browser click.

A complementary Obsidian feature: Settings → Files and links → Attachment folder path can be set to `raw/assets/`, and a hotkey can be bound to "Download attachments for current file" — this downloads all images in a clipped article to local disk, making them available for the LLM to view.

---

## Appearances in Sources

- [[defileo-claude-obsidian-second-brain]] — recommended as the capture tool for web articles

---

## Related Entities & Concepts

- [[obsidian]] — the app this extension integrates with
- [[llm-wiki-pattern]] — the workflow this tool feeds into
