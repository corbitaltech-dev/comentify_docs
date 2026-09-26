---
name: docs-grammar-style
description: Proofreading pass for the Comentify docs — grammar, missing/wrong verbs, singular-plural mismatches, subject-verb agreement, broken sentences, and markdown leaking into frontmatter. Activate on any new or rewritten page before it ships, on a full-site proofreading sweep, or when the user asks to check a page for typos or grammar.
---

# Grammar and style proofreading

A line-by-line proofread, not a lint. The other skills catch mechanical brand/link/format drift; this one catches sentences that are simply wrong. On the WaMatrix.io docs, a careful read found roughly **one error per longer page** — treat that as the base rate here too: a page that reads clean on skim still needs a slow read.

---

## What to check, line by line

- **Every sentence has a verb**, and it's the right one. The classic failure: a bullet expanded into a sentence with the verb dropped. *"When someone comment on your post and it matches, a DM."*
- **Subject-verb agreement**, especially after inserted clauses that change the apparent subject, and "you" clauses drifting into third person.
- **Singular/plural consistency within one sentence.** *"Select one or more post."* → *posts*.
- **Capitalisation of ordinary verbs mid-sentence** — a UI label's capitals bleeding into prose: *"You **Select** a post"* → *select*. Only the bolded UI label keeps its app capitalisation.
- **Article + link text agreement.** *"add a [Keywords](…)"* → *"add a [keyword](…)"*.
- **Dangling or garbled clauses** — often where an edit half-removed a clause. If it doesn't parse aloud, it's broken, not a style nit.
- **Frontmatter is plain text.** `description:` and `keywords:` carry no `**bold**`, no links, no markdown.
- **Consistent spelling within a page.** The site currently mixes US and UK spelling ("behavior", "summarises"). Don't sweep the site — but don't mix within a single page you're editing; match the page's dominant form and flag the site-wide choice to the user once.

## Method

1. Read the page start to finish, at prose speed — not a `grep` pass. Grammar errors share no common substring.
2. For every fix, quote the **current text**, the **fix**, and a one-line reason if not obvious.
3. Don't rewrite voice or restructure while proofreading — that's `docs-writer`'s job. Fix the broken sentence; leave a correct-but-plain one alone.
4. If a sentence is ambiguous about what it means (not just broken), flag it rather than guessing — a confident wrong fix is worse than a flagged sentence.

## Reporting

One table per page: `location — current text — fix`. State the total error count, and separate pages read line-by-line from pages only grep-checked, so `docs-manager` knows which still need a full read.
