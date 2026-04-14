---
type: source
domain: pkm
tags: [claude, obsidian, second-brain, pkm, llm-wiki, automation, tools]
created: 2026-04-13
updated: 2026-04-13
---

# Defileo — "Claude + Obsidian have to be illegal"

> **Type:** X (Twitter) thread  
> **Author:** [[defileo]] (Leo)  
> **Date published:** 2026-04-08  
> **Source file:** `Clippings/(1) Defileo🔮 on X "Claude + Obsidian have to be illegal".md`  
> **Original URL:** https://x.com/defileo/status/2042241063612502162

---

## Summary

Leo's viral X thread is a punchy, practitioner-level popularisation of the [[llm-wiki-pattern]] first articulated by [[andrej-karpathy]]. The central claim is that combining [[claude-code]] with [[obsidian]] produces a "second brain" — a personal knowledge base that knows you, your projects, your tasks, and every article you've ever read, and that gets smarter every day without requiring manual maintenance from you. Unlike most PKM systems that die because maintenance piles up, this setup delegates all bookkeeping to the LLM: the human curates sources and asks questions, Claude does the summarising, cross-referencing, filing, and updating.

The thread is structured as a how-to guide: download Obsidian, create a vault, point [[claude-code]] at it, and paste in [[andrej-karpathy]]'s [[llm-wiki-pattern]] prompt as the schema. Leo embeds the full Karpathy prompt (two-part copy-paste) as the "most important step." Beyond setup, the thread provides concrete, copy-paste CLI prompts for the three core operations — ingest, query, and lint — plus a morning digest automation script. The tone is motivational and direct; the thread is aimed at people who have tried and abandoned [[second-brain]] systems before.

The thread closes with a historical anchor: [[vannevar-bush]]'s 1945 [[memex]] vision — a personal, curated knowledge store where connections between documents are as valuable as the documents themselves. Leo, echoing Karpathy, argues that the LLM finally solves the maintenance problem Bush couldn't: the human thinks, the machine files.

---

## Practical Setup — Step by Step

1. Install [[obsidian]] and create a vault (Leo's is called "Leo's workspace").
2. Install [[claude-code]] for desktop.
3. Open Claude Code and point it at the vault directory.
4. Paste [[andrej-karpathy]]'s [[llm-wiki-pattern]] prompt as the schema/`CLAUDE.md`. *(See [[andrej-karpathy]] and [[llm-wiki-pattern]] pages for the full prompt.)*
5. Start feeding sources into the vault.

> **Note on the Karpathy prompt:** Leo references it as the cornerstone of the setup. It is the same document that was used to initialise this vault. Treated here as a reference rather than re-ingested separately.

---

## Core CLI Prompts

### Ingest
```
claude -p "I just added an article to /raw-sources.
Read it, extract the key ideas, write a summary page to /wiki/summaries/,
update index.md with a link and one-line description, and update any
existing concept pages that this article connects to.
Show me every file you touched." --allowedTools Bash,Write,Read
```

### Lint (weekly health check)
```
claude -p "Read every file in /wiki/. Find: contradictions between pages,
orphan pages with no inbound links, concepts mentioned repeatedly but
with no dedicated page, and claims that seem outdated based on newer files
in /raw-sources/. Write a health report to /wiki/lint-report.md with
specific fixes." --allowedTools Bash,Write,Read
```

### Morning Digest (one-time setup, runs via cron at 7:30am)
```
claude -p "Write a Python script called morning_digest.py that:
1) reads Memory.md and surfaces any open actions due today
2) reads any new files added to /raw-sources in the last 24 hours
3) prints a clean briefing to the terminal.
Then schedule it as a cron job every morning at 7:30am." --allowedTools Bash,Write
```

### Process a Call Transcript
```
claude -p "Read the transcript in /transcripts/call-today.md.
Extract every decision made, every action item with owner and deadline,
and a 3-bullet summary. Add actions to /Action-Tracker.md, log decisions
to /Decision-Log.md, and create a client note in /clients/ linking back
to this transcript." --allowedTools Bash,Write,Read
```

---

## Key Claims

- One ingest command causes Claude to touch 10–15 wiki pages, surface unexpected connections, flag contradictions, and log every change.
- The reason most [[second-brain]] systems fail: maintenance burden grows faster than value — people stop, the system degrades, the cycle repeats. Claude breaks this permanently.
- Obsidian is optional as a UI; you can work entirely from the terminal and Obsidian is just "the window you look through."
- A `Memory.md` file — a structured summary of who you are, your goals, and your projects — is enough context to make Claude feel like it "knows you" from the first session.
- Migrating from Notion or reorganising an entire vault can be done with a single prompt.

---

## Notable Quotes

> "That's not a chatbot, that's a second brain that never sleeps, never forgets, and gets smarter every single day you use it."

> "The human's job is to curate sources, ask good questions, and think about what it all means. Claude's job is everything else."

> "Maintenance stops being your job."

> "Build this once → Use it forever, and it gets better every single day you add to it."

---

## Concepts Introduced or Discussed

- [[llm-wiki-pattern]] — the underlying architecture Leo is implementing
- [[second-brain]] — the PKM framework this builds on
- [[rag]] — the approach this replaces / contrasts with
- [[memex]] — Vannevar Bush's 1945 vision, cited as the spiritual ancestor
- [[morning-digest-automation]] — the cron-based daily briefing pattern

---

## Entities Mentioned

- [[defileo]] — author of this thread
- [[andrej-karpathy]] — originator of the LLM Wiki pattern; his prompt is the schema
- [[obsidian]] — the markdown vault / UI layer
- [[claude-code]] — the LLM agent that maintains the wiki
- [[vannevar-bush]] — historical reference; creator of the Memex concept
- [[obsidian-web-clipper]] — browser extension for clipping articles into raw sources

---

## Open Questions & Gaps

- Leo mentions a `Memory.md` file as a way to give Claude context about who you are — this pattern is not detailed further. Worth exploring as a separate concept.
- The morning digest script is described but not shown in full; Claude generates it on demand.
- No detail on how to handle image-heavy sources or PDFs specifically.
- Query workflow is mentioned but not demonstrated with a concrete prompt example.

---

## Related Sources

*(none yet — first source in the wiki)*
