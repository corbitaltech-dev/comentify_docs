# Documentation project instructions

## About this project

- This is the Comentify documentation site (`docs.comentify.io`), built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`; custom CSS in `style.css`
- Pushing to `master` deploys the live site

## Terminology, style, and content boundaries

The real rules — banned words and jargon, brand naming ("Comentify"), voice, page
structure, Meta-citation requirements, and the facts still waiting to be verified —
live in **`.claude/skills/comentify-docs/SKILL.md`**. Read that file before writing or
editing any page; it is the single source of truth, not this file.

Related skills for specific tasks: `docs-fact-check` (verify a claim against the
product), `docs-competitor-benchmark` (benchmark against ManyChat/LinkDM/CreatorFlow/
Inrō), `docs-from-notes` (draft a page from bullets + screenshots),
`docs-consistency-lint` / `docs-grammar-style` / `docs-link-integrity` / `docs-audit`
(QA sweeps), and the `docs-manager` agent (runs the sweeps and routes fixes).
See `.claude/README.md` for the full map.
