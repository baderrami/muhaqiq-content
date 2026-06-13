# Content schema

Every file has YAML frontmatter + a markdown body. The body is the prose/dossier.

## Common frontmatter (all types)

| Field | Required | Notes |
|---|---|---|
| `id` | yes | system-wide ID; must equal the filename. `P-####` / `C-####` / `F-####` |
| `type` | yes | `person` \| `case` \| `fact` |
| `title` | yes | display label (not the identity — the ID is) |
| `created` | yes | ISO date `YYYY-MM-DD` |
| `edges` | no | list of `{ to: <ID>, rel: <relation> }` — referenced IDs must exist |

## Fact-only frontmatter

| Field | Required | Notes |
|---|---|---|
| `claim_type` | yes | `fact` \| `claim` \| `opinion` (opinions get no credibility status) |
| `sources` | yes (≥1) | list of `{ url, tier }` |

`tier` ∈ `primary` (official/court/sanctions doc) · `reporting` (named journalism) · `tip` (anonymous; never eligible for "corroborated").

## Relations (`rel`)

`involves` / `involved_in` (case ↔ person) · `about` (fact → subject) · `part_of` (fact → case) ·
`supports` / `refutes` / `context` (fact → fact).

## NOT in this repo

- **status / bridging score** — computed from votes in the app's private Postgres DB, overlaid at render.
- **votes, contributor identity, moderation internals** — app side only.

## CI validation (enforced on every PR)

- `id` matches filename and is unique
- every `edges[].to` and `sources` present/valid
- facts have ≥1 source; allegations about living people need a `primary` or `reporting` source
