# muhaqiq-content

The **public, versioned content ledger** for [مُحقِّق / Muhaqiq](https://muhaqiq.org) — an open
community fact-verification board.

Every person, case, and fact is **one markdown file** with YAML frontmatter. Files are named by a
**system-wide ID** and reference each other **by ID** (never by embedding). The app maps each file
to a typed object (gray-matter + Zod). Additions and edits arrive as **Pull Requests**; the git
history is the public audit log.

```
people/   P-####.md     persons
cases/    C-####.md     cases / files
facts/    F-####.md     sourced facts
```

- **IDs are the primary key.** Filename = ID (`facts/F-3318.md`).
- **Edges reference by ID** — e.g. a fact's `edges: [{ to: P-1042, rel: about }]`.
- **Sources are mandatory on facts**, with a `tier` (primary / reporting / tip).
- **Bridging status is NOT stored here.** It is computed from votes in the app's private DB and
  overlaid at render time, so this repo stays pure facts + provenance.

See [SCHEMA.md](./SCHEMA.md) for the full schema. Content is authored as if already public
(no private data in history).
