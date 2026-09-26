---
name: docs-consistency-lint
description: Site-wide sweep for brand, banned-word, formatting, and time-promise drift on the Comentify docs — misspelled "Commentify", developer jargon (OAuth, access token, Graph API, webhook) on customer pages, "tenant" instead of "workspace", "no coding required" reassurance, specific limits or prices outside the plans page, thin or missing image alt text, Font Awesome icon names and missing sidebar icons, Title Case vs sentence case drift, inconsistent UI-label casing, and setup-time promises. Activate for a pre-launch sweep, a scheduled docs-manager run, or 'lint this page/section for brand and formatting issues'.
---

# Consistency lint: brand, banned words, formatting, time promises

A mechanical pass over the rules in `comentify-docs` §1, §2, §4, §5. Grep the whole site, don't sample. Every section below is a reproducible check; run the command, don't eyeball it. Run from the repo root.

Read `comentify-docs` first — this skill only *finds* violations of its rules; it doesn't restate the reasoning.

---

## §1 — Banned words in body prose

```bash
grep -rn --include="*.mdx" -w "tenant" .
grep -rn --include="*.mdx" -wE "provisioning|instantiate|quota|entitlement" .
grep -rn --include="*.mdx" -wiE "leverage|utilise|utilize|seamless|seamlessly|robust|powerful|scalable" .
grep -rn --include="*.mdx" -iE "no coding|without (any )?code|no technical|don't need a developer" .
```

Mechanical fix: swap for the house term (full table in `comentify-docs` §1). For "no coding required", delete the phrase and keep the rest of the sentence.

## §2 — Brand spelling

```bash
grep -rniE --include="*.mdx" "commentify" .                  # misspelling, any case
grep -rnE --include="*.mdx" "(^|[^@/.\[])Comentify\.io\b" .   # domain used as the brand name in prose
```

Every hit should read **Comentify**. Lower-case `comentify.io` inside a URL, link text or email address is correct and not matched.

## §3 — Developer jargon on customer pages (judgement — escalate)

```bash
grep -rniE --include="*.mdx" "\bOAuth\b|access token|Graph API|\bwebhooks?\b|\bendpoints?\b|\bpayload\b|\bscopes?\b|\bIGSID\b|\bPSID\b|Business Account ID" .
```

A hit here is a **plain-language pass**, not a find-replace — the sentence was usually built around the jargon. Report it and route to `docs-writer`. Exception: a literal field label the user must copy from the real UI, confirmed via `docs-fact-check`.

## §4 — Icons

Font Awesome names render as nothing, silently.

```bash
# Font Awesome names known to slip in
grep -rnE --include="*.mdx" 'icon[=:] *"(bolt|comments?|comment-dots|message|diagram-project|paper-plane|wand-magic-sparkles|pen-to-square|clock-rotate-left|shield-halved|chart-bar|user-tie|note-sticky|robot|bullhorn|address-book|file-lines|mobile)"' .
grep -nE '"icon": *"(bolt|comments|robot|bullhorn|diagram-project)"' docs.json
# pages with no sidebar icon
grep -rL --include="*.mdx" "^icon:" . | grep -v "^./snippets/"
```

Full known-bad → correct table is in `comentify-docs` §5. After any fix, load the page in `mint dev` and **look** — a plausible-looking name can still not exist in Lucide.

## §5 — Time promises

```bash
grep -rniE --include="*.mdx" "in (a |just |only )?(few|a couple of|[0-9]+|ten|five) (minutes|seconds|hours)|in minutes|under (10|ten|[0-9]+) minutes|within (a few )?seconds|set up in|takes only|ready in|instantly" .
```

Triage each hit:
- **Our own speed claim** ("go live in under 10 minutes", "within a few seconds Comentify replies") → delete the timing, keep the rest.
- **A factual, non-promise duration** from Meta (a messaging window, a reconnection period) → leave it, but it needs a Meta citation (`comentify-docs` §6).

## §6 — Limits and prices outside the plans page

```bash
grep -rnE --include="*.mdx" "[\$€£₹] ?[0-9]|[0-9,]+ (DMs|messages|accounts|automations|seats|contacts|leads)( a| per)? (month|day|hour)?|[0-9]+ days" . | grep -v "^./account/plans.mdx"
```

Every hit outside `account/plans.mdx` is a finding: replace the number with a description and a link to [Plans](/account/plans). A Meta-imposed number (a messaging window) stays only if cited.

## §7 — Image alt text

```bash
grep -rn --include="*.mdx" -E '!\[.{0,25}\]\(' .
grep -rn --include="*.mdx" -E '<BrowserFrame[^>]*alt=""' .
```

Flag an image whose `alt` is empty or just the feature name rather than a description of what's on screen.

## §8 — UI-label casing consistency

The same button referred to with two capitalisations ("New rule" vs "New Rule"). No single grep finds these; they surface on a close read. Once you spot one:

```bash
grep -rn --include="*.mdx" -i "new rule" .
```

The **real UI label** (confirmed via `docs-fact-check`) wins; make every reference match it exactly.

## §9 — Title Case vs sentence case

House rule (`comentify-docs` §4) is sentence case for titles and headings.

```bash
grep -rnE --include="*.mdx" '^title: "([A-Z][a-z]*\s+){2,}' .
grep -rnE --include="*.mdx" '^#{2,3} ([A-Z][a-z]*\s+){2,}[A-Z]' .
```

The heuristic over-matches (proper nouns, product names like "Shared Inbox" if that's the real UI label) — **read every hit**. As of 2026-09-26 the whole site is Title Case, so the first fix is a site-wide decision: **escalate to the user once**, then apply mechanically.

---

## Reporting

A flat list grouped by section, each line `file:line — current text — proposed fix`. Separate **mechanical** hits (§1, §2, §4, §5 own-speed claims, §6, §7) from **judgement** hits (§3, §8, §9) — `docs-manager` uses this split to decide auto-fix vs escalate. State "zero hits" explicitly for a clean section so the reader knows it was checked, not skipped.
