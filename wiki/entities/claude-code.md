---
type: entity
domain: pkm
tags: [tool, ai, llm, anthropic, agent]
created: 2026-04-13
updated: 2026-04-13
sources: [defileo-claude-obsidian-second-brain]
---

# Claude Code

Anthropic's agentic CLI tool; the LLM layer that reads, writes, and maintains the wiki in the [[llm-wiki-pattern]] setup.

---

## Overview

Claude Code is a command-line AI agent built by Anthropic. It can read files, write files, run shell commands, and reason across large amounts of context — making it well-suited to operating as the "programmer" in a markdown wiki system. In this vault, Claude Code is the tool executing every ingest, query, lint, and maintenance operation.

---

## Key Facts

| Attribute | Value |
|-----------|-------|
| Type | CLI agent / desktop app |
| Developer | Anthropic |
| Key capability | File read/write + shell access + large context window |
| Schema file | `CLAUDE.md` (governs behaviour in this vault) |

---

## What the Wiki Knows

In the [[llm-wiki-pattern]], Claude Code's role is as the **writer and maintainer** of the wiki. The human points it at a vault directory; `CLAUDE.md` tells it the conventions, workflows, and rules. From there, Claude Code handles all the bookkeeping: summarising sources, creating and updating pages, maintaining cross-references, running lint checks, and logging every operation.

[[defileo]] notes that Claude Code can be invoked headlessly via the `-p` flag with `--allowedTools` to restrict what it can do, making automated workflows (cron jobs, scheduled ingests) straightforward. The `Memory.md` pattern — a file describing who the user is, their goals, and open projects — gives Claude Code enough context to feel personalised from the first prompt of each session.

Key operational modes (per [[defileo-claude-obsidian-second-brain]]):
- **Ingest:** reads a new source, updates 10–15 wiki pages, logs all changes
- **Query:** reads the index and relevant pages, synthesises an answer with citations
- **Lint:** scans the entire wiki for contradictions, orphans, stale claims, missing pages
- **Transcript processing:** extracts decisions and actions from meeting transcripts into structured trackers

---

## Appearances in Sources

- [[defileo-claude-obsidian-second-brain]] — the LLM agent central to the entire setup

---

## Related Entities & Concepts

- [[obsidian]] — the UI layer Claude Code writes into
- [[llm-wiki-pattern]] — the architecture Claude Code implements
- [[andrej-karpathy]] — originator of the pattern Claude Code is used to execute
- [[morning-digest-automation]] — an automated Claude Code workflow
