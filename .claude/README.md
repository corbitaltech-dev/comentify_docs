# Comentify docs — the `.claude/` layer

This folder holds the agents and skills that write, draft, and monitor the customer-facing documentation at `docs.comentify.io`. It's two layers on top of one shared rulebook.

Ported on 2026-09-26 from the WaMatrix.io docs layer (`docs.whatsmark.io/.claude/`), which was built from a real site audit. The method carries over unchanged; the Comentify-specific facts that haven't been verified yet are listed in `skills/comentify-docs/SKILL.md` §0 — resolve those first.

---

## Layout

```
.claude/
├── agents/
│   ├── docs-writer.md         — general-purpose author: write, rewrite, review, fact-check any page
│   ├── docs-drafter.md        — turns short bullet notes + screenshots into a finished page
│   ├── docs-reviewer.md       — QA gate: pass/fail punch list on a changed page or PR
│   └── docs-manager.md        — master agent: runs the full audit, auto-fixes what's safe, routes the rest
├── skills/
│   ├── comentify-docs/SKILL.md            — the rulebook: voice, brand, banned words, structure, Mintlify mechanics
│   ├── docs-fact-check/SKILL.md           — verify a claim against the product
│   ├── docs-competitor-benchmark/SKILL.md — benchmark against ManyChat, LinkDM, CreatorFlow, Inrō
│   ├── docs-from-notes/
│   │   ├── SKILL.md                — method: short notes + screenshots → full on-brand page
│   │   └── INTAKE-TEMPLATE.md      — fill one per feature
│   ├── docs-consistency-lint/SKILL.md     — brand, banned words, jargon, icons, numbers, time promises, casing
│   ├── docs-grammar-style/SKILL.md        — proofreading pass
│   ├── docs-link-integrity/SKILL.md       — links, anchors, image paths, docs.json, Meta soft-404s
│   └── docs-audit/
│       ├── SKILL.md                — full-site health sweep + report template + severity model
│       └── reports/                — dated audit reports land here
```

## How the layers fit together

| Layer | Files | Job |
| --- | --- | --- |
| **Rulebook** | `comentify-docs` | Voice, banned words, brand, mechanics, Meta citations, shared-repo safety, checklist |
| **Writing** | `docs-writer` + `docs-fact-check`, `docs-competitor-benchmark` | Author and fact-check pages |
| **Drafting from notes** | `docs-drafter` + `docs-from-notes` (+ `INTAKE-TEMPLATE.md`) | Turn bullets + screenshots into a finished page |
| **Monitoring / QA** | `docs-manager` + `docs-reviewer` + the 4 monitoring skills | Keep the site healthy; gate every change |

Every file points back to `comentify-docs` as the single source of truth.

## How to use it

- **Draft a page from your notes:** fill `docs-from-notes/INTAKE-TEMPLATE.md`, attach screenshots, hand both to `docs-drafter`.
- **Author a page from scratch:** ask `docs-writer`.
- **Before you publish / on a PR:** run `docs-reviewer` on the changed files.
- **Weekly, or after any reorg:** run `docs-manager`.
- **One-off:** invoke a skill directly, e.g. "run docs-consistency-lint on `automation/`".

## The one rule that makes this safe

**Auto-fix only the unambiguous, mechanical things; escalate everything with a judgement, a fact, or a voice rewrite.** The split is defined once, in `docs-manager`. Pushing to `master` deploys the live site, so sweep fixes go on a branch.
