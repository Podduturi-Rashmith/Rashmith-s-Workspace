# CLAUDE.md — LLM Wiki Schema

This file is the operating manual for this Obsidian vault. Read it at the start of every session before doing anything else. It defines the directory layout, page conventions, and step-by-step workflows for ingesting sources, answering queries, and maintaining the wiki.

---

## Directory Layout

```
/
├── CLAUDE.md                  ← this file; the LLM's operating manual
├── raw/                       ← immutable source documents (never modify)
│   ├── assets/                ← downloaded images referenced by sources
│   └── <source files>         ← articles (.md), PDFs, text files, etc.
└── wiki/                      ← LLM-owned; everything here is generated/maintained by the LLM
    ├── index.md               ← master catalog of all wiki pages (update on every ingest)
    ├── log.md                 ← append-only chronological record of all operations
    ├── overview.md            ← high-level synthesis across all domains; update periodically
    ├── _templates/            ← page templates (do not link to these from other pages)
    │   ├── source.md
    │   ├── entity.md
    │   └── concept.md
    ├── sources/               ← one page per ingested source
    ├── entities/              ← people, companies, books, products, places, projects
    ├── concepts/              ← ideas, topics, themes, frameworks, events
    ├── domains/               ← domain-level overviews (e.g. "Machine Learning", "Finance")
    └── queries/               ← filed answers to notable questions asked by the user
```

**The golden rule:** `raw/` is read-only. The LLM writes only inside `wiki/`. Never modify source files.

---

## Page Types

### `wiki/sources/<slug>.md`
One page per ingested source. Captures what the source says without heavy editorialising.

### `wiki/entities/<slug>.md`
A page for any named thing that appears across multiple sources or is significant on its own: a person, company, book, product, place, project, technology, dataset. Update these when new sources add information.

### `wiki/concepts/<slug>.md`
A page for an idea, topic, theme, framework, or event. More abstract than entities. Update these as understanding deepens.

### `wiki/domains/<slug>.md`
High-level overview of a domain (e.g. "personal-research", "books", "competitive-analysis", "projects"). Summarises the state of knowledge across all sources in that domain. Update after ingesting sources that belong to the domain.

### `wiki/queries/<slug>.md`
A filed answer to a notable question the user asked. Created when an answer is substantial enough to be worth keeping. Linked from `index.md`.

### `wiki/overview.md`
A bird's-eye synthesis across the entire vault. Updated periodically during lint passes or when the user requests it.

---

## Naming Conventions

- File names: lowercase, hyphenated, no spaces. E.g. `alan-turing.md`, `attention-mechanism.md`.
- Source pages: name after the source. E.g. `the-pragmatic-programmer.md`, `openai-o3-announcement.md`.
- Entity and concept pages: name after the thing itself.
- Domain pages: broad, readable labels. E.g. `machine-learning.md`, `personal-health.md`.
- Slugs should be stable — don't rename pages once created, as other pages link to them.

---

## Frontmatter

Every wiki page (except `index.md`, `log.md`, `overview.md`) should have YAML frontmatter:

```yaml
---
type: source | entity | concept | domain | query
domain: <primary domain, e.g. "books", "research", "projects">
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [slug1, slug2]        # for entity/concept pages: which sources informed this page
---
```

- `type` is always one of the five values above.
- `domain` is free-form but should be consistent (pick one primary domain per page).
- `tags` are free-form; use them for Obsidian Dataview queries.
- `sources` on entity/concept pages: list the source slugs that contributed to this page.

---

## Cross-Referencing

- Use Obsidian wiki-links: `[[page-name]]` or `[[page-name|Display Text]]`.
- Every entity or concept mentioned significantly on a page should be linked on first mention.
- Source pages should link to every entity and concept they introduce or discuss.
- Entity/concept pages should link back to the source pages they draw from.
- Domain pages should link to all entities, concepts, and sources in that domain.
- `index.md` links to every page in the wiki.
- Orphan pages (no inbound links from other wiki pages) are a lint issue.

---

## Workflows

### 1. Ingest Workflow (one source at a time)

When the user says "ingest [source]" or drops a file in `raw/` and asks you to process it:

**Step 1 — Read.**
Read the source file thoroughly. If it references images, read the text first, then view images that seem important for understanding. For PDFs, read page by page.

**Step 2 — Discuss.**
Before writing anything, summarise the key takeaways for the user in 3–7 bullet points. Ask:
- "What aspect should I emphasise most?"
- "Is there anything here you want me to ignore or treat differently?"
- "Which domain does this belong to?"

Wait for the user's response before proceeding.

**Step 3 — Write the source page.**
Create `wiki/sources/<slug>.md` using the source template. Include:
- A 2–3 paragraph summary in your own words
- Key claims, data points, frameworks introduced
- Notable quotes (with page/paragraph reference if available)
- Questions or gaps the source leaves open
- Links to all entities and concepts mentioned

**Step 4 — Update entity and concept pages.**
For each significant entity or concept in the source:
- If a page exists: open it, add new information from this source, update the `sources` frontmatter list, update `updated` date, add a cross-link to the source page.
- If no page exists: create one using the appropriate template.

A single source will typically touch 5–15 entity/concept pages. That's normal and expected.

**Step 5 — Update the domain overview.**
Open (or create) the relevant `wiki/domains/<domain>.md` page. Add a line or paragraph noting what this source contributed to the domain's understanding. Update the source list at the bottom.

**Step 6 — Update `wiki/index.md`.**
Add the new source page to the Sources section. Add any new entity/concept/domain pages to their sections. Keep entries to one line: `[[page-name]] — one-sentence description`.

**Step 7 — Append to `wiki/log.md`.**
Add an entry at the top of the log (most recent first):
```
## [YYYY-MM-DD] ingest | <Source Title>
- Source: `raw/<filename>`
- Summary: <one sentence>
- Pages created: <list>
- Pages updated: <list>
```

**Step 8 — Report back.**
Tell the user: what was created, what was updated, anything surprising or notable from the source, and suggest 1–2 follow-up questions worth exploring.

---

### 2. Query Workflow

When the user asks a question about the wiki's contents:

**Step 1 — Search.**
Read `wiki/index.md` to identify relevant pages. Then read those pages.

**Step 2 — Synthesise.**
Answer the question, citing wiki pages with `[[page-name]]` links. Be explicit about what the wiki does and doesn't know. Flag gaps.

**Step 3 — Offer to file.**
If the answer is substantial (more than a few sentences), ask: "Should I file this as a query page?" If yes, create `wiki/queries/<slug>.md` and add it to `index.md` and `log.md`.

---

### 3. Lint Workflow

When the user says "lint the wiki" or "health-check":

Check for and report:
1. **Orphan pages** — pages with no inbound links from other wiki pages (excluding index.md).
2. **Contradictions** — claims on different pages that conflict; flag them explicitly.
3. **Stale claims** — information on a page that newer sources have superseded.
4. **Missing pages** — entities or concepts mentioned across pages but lacking their own page.
5. **Broken or missing cross-references** — significant entities mentioned but not linked.
6. **Thin pages** — pages with fewer than 3 substantive sentences; flag for enrichment.
7. **Domain gaps** — domains with very few sources; suggest new sources to look for.

Produce a lint report as a markdown checklist. Ask the user which issues to fix now vs. later. Fix the ones they want fixed immediately.

---

### 4. Overview Update

When the user says "update the overview":

Read all domain pages and `index.md`. Rewrite `wiki/overview.md` to reflect the current state of the entire vault — what domains are covered, what the major themes are, what the key open questions are. Keep it to 1–2 pages.

---

## Log Format

`wiki/log.md` is append-only (new entries go at the top). Each entry starts with:
```
## [YYYY-MM-DD] <operation> | <title>
```

Operations: `ingest`, `query`, `lint`, `overview`, `manual`.

This prefix format makes log entries greppable: `grep "^## \[" wiki/log.md | head -20`

---

## Session Start Checklist

At the start of every new session:
1. Read this file (`CLAUDE.md`) fully.
2. Read `wiki/index.md` to orient yourself to the current state of the wiki.
3. Read the last 5 entries of `wiki/log.md` to see what was done recently.
4. Greet the user with a one-line status: how many pages exist, what was last ingested.

---

## House Rules

- Never modify files in `raw/`. Ever.
- Always update `index.md` and `log.md` after any write operation on the wiki.
- Prefer updating existing pages over creating new ones (avoid fragmentation).
- When in doubt about whether something deserves its own page, create it — pages are cheap and the index keeps them findable.
- Do not create pages in `_templates/` — those are templates only.
- Use today's date (from context or ask the user) in frontmatter and log entries.
- Write in a clear, neutral, encyclopaedic tone on wiki pages. Save opinions for the `queries/` section when asked.
- Page length: source pages 300–800 words; entity/concept pages 150–500 words; domain pages 100–300 words.
