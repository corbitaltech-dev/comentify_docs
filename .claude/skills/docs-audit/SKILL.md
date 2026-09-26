---
name: docs-audit
description: Full-site health sweep for the Comentify docs — runs the consistency, grammar, and link-integrity checks across every page, deep-reads a representative sample per section, and produces a severity-ranked report with a suggested order of work. Activate for a pre-launch review, a scheduled full sweep (docs-manager runs this weekly or after any reorg), or when the user asks for a health check / audit of the docs site.
---

# Full-site documentation audit

The site-wide health check. It combines the mechanical sweeps (`docs-consistency-lint`, `docs-grammar-style`, `docs-link-integrity`) with a deep, line-by-line read of a representative sample, then reports everything in one severity-ranked document. Every check defers to `comentify-docs` for the *rule* and to the three checking skills for *how to find violations*; this skill owns the **process and the report shape**.

---

## 1. How to run it

1. **Read the governance files first**, every time — `AGENTS.md` and `.claude/skills/comentify-docs/SKILL.md`, including its §0 "Facts to confirm" table. Rules change.
2. **Deep-read a representative sample**: `introduction.mdx`, `quickstart.mdx`, `connecting-accounts.mdx`, `account/plans.mdx`, and one page from each nav group. Read these **in full**, line by line.
3. **Run every mechanical check site-wide** — don't sample these:
   - `docs-consistency-lint`
   - `docs-link-integrity`
   - `docs-grammar-style` on at least the deep-read sample; note which pages were *not* read line-by-line.
4. **Note what's already good.** Always include a "keep doing this" section naming specific pages and patterns.

## 2. Severity and effort model

| Severity | Meaning |
|---|---|
| **High** | Breaks the reader's task now — a 404, a paywall surprise, a wrong factual claim (a button that doesn't exist, a wrong retention or refund term). |
| **Medium** | Undermines trust or consistency but doesn't stop the reader — brand slips, jargon, time promises, casing drift, grammar errors. |
| **Low** | Internal hygiene with no reader-facing impact. |

| Effort | Meaning |
|---|---|
| **Trivial** | A single-line fix, no judgement. |
| **Low** | A find-replace across a handful of files, no judgement. |
| **Medium** | Rewriting a sentence or paragraph; unambiguous once decided. |
| **Needs a decision** | Depends on a product/IA call only the user can make. Never resolve these unilaterally. |

Bucket findings by lettered theme — flagship self-consistency, broken links, brand/banned words, unverified facts, formatting, grammar, information architecture, repo hygiene — and reuse the same letters across audits so successive reports are diffable.

## 3. Report template

Save to `.claude/skills/docs-audit/reports/YYYY-MM-DD-audit.md`.

```markdown
# Comentify Documentation Audit

**Site:** docs.comentify.io (Mintlify)
**Date:** <date>
**Status:** <pre-launch / live / post-reorg>
**Audited against:** .claude/skills/comentify-docs/SKILL.md

## 1. How this audit was done
<governance files read, pages deep-read, sweeps run>

## 2. Reproduce / verify before shipping
<every grep/mint/python command used>

## 3. Executive summary
<one paragraph, plus the severity × effort table of lettered buckets>

## 4. Findings
<one subsection per bucket; each finding: what, where (file:line), why it matters, fix>

## 5. What's already good (keep doing this)
<specific pages/patterns — not optional>

## 6. Suggested order of work
<cheapest-and-highest-severity first, decisions last>

## 7. Time-promise and number check
<explicit pass over comentify-docs §2 — time promises and limits/prices outside the plans page>

## 8. Facts-to-confirm status
<each row of comentify-docs §0: still open / resolved on <date>>
```

## 4. Findings vs. escalations

- **Mechanical** (banned words, brand spelling, icon typos, dead old-path links, own-speed time promises) — state the fix directly.
- **Judgement** (jargon rewrites, sentence case as a site convention, duplicate pages, folder renames, anything depending on an unverified product fact) — state the **options**, mark "needs a decision", don't pick.

## 5. Common finding categories (checklist)

- Flagship self-consistency — the intro or quick start contradicting itself or another page.
- Unverified product facts — labels, nav paths, plan gates, retention/refund terms (`comentify-docs` §0).
- Broken links from a reorg — see `docs-link-integrity` §2.
- Brand / banned-word / jargon slips — `docs-consistency-lint` §1–3.
- Formatting — icons, alt text, heading casing — `docs-consistency-lint` §4, §7–9.
- Grammar — `docs-grammar-style`.
- Information architecture — a nav group that tells the reader nothing, or two pages covering the same feature.
- Repo hygiene — files that shouldn't be published leaking into the build, remote assets that may vanish.
- Time promises and numbers — check separately; easy to under-grep.

## 6. After the audit ships

The report is not the fix. `docs-manager` takes it, auto-fixes what's mechanical on a scoped branch, and routes the rest (voice rewrites to `docs-writer`, unverified facts to `docs-fact-check`, decisions to the user). A repeat audit that finds the same mechanical issues means the routing step didn't happen.
