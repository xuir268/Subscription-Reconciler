# LLM Wiki

A personal knowledge base maintained by an LLM agent. See `CLAUDE.md` for the
schema, page conventions, and ingest/query/lint workflows the agent follows.

## Opening this as an Obsidian vault

Open the `llm-wiki/` folder itself as the vault root — not the repo root —
so Obsidian's graph view and backlinks only cover wiki content, not Go source.

**On the Mac:**

1. Clone the repo normally in Terminal: `git clone <repo-url>`.
2. In Obsidian, **Open another vault → Open folder as vault**, and pick the
   `llm-wiki` folder inside the clone.
3. Syncing is just git — `git pull` to pick up agent commits, `git add / commit
   / push` for your own edits. No plugin required, though **Obsidian Git** is
   still handy if you want pull/push buttons inside the app instead of
   switching to Terminal.
4. Web Clipper works natively here (it's a desktop browser extension) — use it
   to drop articles straight into `raw/`.

**On the iPad:**

1. Get this repo onto the iPad's local filesystem. Obsidian doesn't speak git
   natively, so use a Git client that exposes files to the Files app / iCloud
   Drive — e.g. **Working Copy** (clone the repo, enable "Export to Files App").
2. In Obsidian, **Open another vault → Open folder as vault**, and pick the
   `llm-wiki` folder inside the cloned repo.
3. To sync changes both ways (agent edits on one side, you edit in Obsidian on
   the other), either:
   - Use Working Copy's UI to pull/push/commit, or
   - Install the **Obsidian Git** community plugin so you can commit/push/pull
     from inside Obsidian itself.
4. Getting sources in on iPad: there's no Web Clipper browser extension on
   iOS, but Obsidian supports the **system share sheet** — share a page/article
   from Safari directly into Obsidian, or into `raw/` via the Files app, then
   tell the agent to ingest it.

If you use both devices against the same vault, treat git as the source of
truth — pull before you start editing on either one to avoid merge conflicts
in the markdown files.

## Using Obsidian effectively here

- **Graph view** is the fastest way to see wiki health at a glance — hub pages
  (well-connected), orphans (isolated nodes worth flagging in a lint pass), and
  clusters that hint at concepts worth their own page.
- **Backlinks panel** (bottom of any page) shows what already links here —
  check it before asking the agent to re-derive context that already exists.
- Frontmatter (`tags`, `created`, `updated`, `sources`) is added by the agent
  on every page; if you want **Dataview**-style tables/queries over it, install
  the Dataview community plugin.
- Keep `index.md` and `log.md` open in a pinned tab — they're the two files
  you and the agent both read first.
