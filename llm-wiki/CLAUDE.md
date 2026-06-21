# LLM Wiki — Schema & Conventions

This directory is a personal knowledge base maintained by an LLM agent, following
the "LLM Wiki" pattern: raw sources stay immutable, the wiki is the LLM-owned
synthesis layer, and this file is the schema the agent follows.

Open this folder (`llm-wiki/`) directly as an Obsidian vault — not the repo root.

## Layout

- `raw/` — immutable source documents (articles, notes, PDFs, transcripts).
  Never edit files here. `raw/assets/` holds downloaded images referenced by sources.
- `wiki/` — LLM-owned markdown pages. Subdirectories:
  - `wiki/entities/` — people, organizations, products, tools — one page per entity.
  - `wiki/concepts/` — ideas, themes, recurring topics.
  - `wiki/sources/` — one summary page per ingested source, linking back to `raw/`.
  - `wiki/overview.md` — the evolving top-level synthesis. Keep this current.
- `index.md` — catalog of every wiki page: link, one-line summary, category, date.
  Update this on every ingest. When answering a query, read this first.
- `log.md` — append-only chronological record. Each entry starts with
  `## [YYYY-MM-DD] <ingest|query|lint> | <title>` so it stays greppable
  (`grep "^## \[" log.md | tail -5`).

## Page conventions

- Every wiki page gets YAML frontmatter: `tags`, `created`, `updated`, `sources`
  (list of source page links it draws from).
- Link liberally with `[[wikilink]]` syntax — Obsidian renders backlinks and the
  graph view from these. An unlinked page is a bug, not a feature.
- When a new source contradicts an existing claim, don't silently overwrite it.
  Note the contradiction explicitly on the relevant page (date both claims) and
  let the user decide how to resolve it.

## Workflows

**Ingest**: read the new source in `raw/`, discuss key takeaways with the user,
write/update its `wiki/sources/` summary page, update every entity/concept page
it touches, update `index.md`, append to `log.md`.

**Query**: read `index.md` first to find candidate pages, drill into them, answer
with citations to specific wiki pages (and raw sources where relevant). If the
answer is itself valuable (a comparison, an analysis), offer to file it back into
the wiki as a new page rather than letting it live only in chat.

**Lint**: periodically scan for contradictions between pages, stale claims
superseded by newer sources, orphan pages with no inbound links, concepts
mentioned repeatedly but lacking their own page, and missing cross-references.

## Notes for this vault

- No search tooling yet — at this scale `index.md` is sufficient. Revisit if the
  wiki grows past ~100 sources.
- Images: read the source text first, then view referenced images from
  `raw/assets/` separately if needed — LLMs can't read inline markdown images in
  one pass.
