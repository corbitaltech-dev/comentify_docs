---
name: docs-link-integrity
description: Finds and fixes broken links on the Comentify docs — stale internal paths left behind by a section reorg, anchors, dead image references, docs.json validity, and Meta/Instagram/Facebook help and developer links that redirect or return a soft-404 (HTTP 200 with an empty shell) which curl and mint broken-links cannot detect. Activate after any folder rename or navigation reorg, before launch, on a scheduled docs-manager sweep, or when a reader reports a dead link.
---

# Link integrity: internal, image, and Meta links

Three distinct failure modes, three distinct checks. `mint broken-links` catches the first two; it cannot catch the third.

---

## §1 — Internal links (authoritative check)

```bash
mint broken-links
```

Ground truth for internal `href`s and anchors. Run it **before and after** any change and report both counts — "2 broken links, both pre-existing" vs. just "2 broken links".

## §2 — Stale paths after a reorg

A folder move or nav reorg leaves the **old path** referenced in cards, prose links and accordions across the site. On WaMatrix.io, every reorg-rot hit turned out wider than the first grep — treat one hit as a signal to sweep the whole repo.

```bash
# after any rename old/path -> new/path
grep -rn --include="*.mdx" "old/path" .
```

Cross-check every hit against the navigation in `docs.json` — a link is only stale if its target isn't a page anymore. Prefer a `docs.json` redirect for URLs that may have been shared externally.

## §3 — Anchors

Card links like `/inbox/shared-inbox#conversation-view` depend on a heading that produces that slug. Renaming a heading silently breaks them.

```bash
grep -rnoE --include="*.mdx" 'href="/[^"#]+#[^"]+"' .
```

For each, confirm the target page has a heading whose slug matches.

## §4 — Image references

```bash
grep -rn --include="*.mdx" "!\[" .
grep -rn --include="*.mdx" 'src="' .
```

For each local `src`, confirm the file exists at that path. Remote images (e.g. the `media.brand.dev` logo and favicon in `docs.json`) can disappear without warning — flag any remote asset, and prefer committing a copy into the repo.

## §5 — `docs.json` validity

```bash
python3 -c "import json; json.load(open('docs.json')); print('valid')"
mint validate
```

Run after *any* edit to `docs.json`. It's the file most likely to be mid-edit by another writer, and a syntax error breaks the whole site's navigation. (The "Error generating favicons" warning from `mint validate` is pre-existing — the favicon is a remote URL.)

## §6 — Meta/Instagram/Facebook links: soft-404s and redirects

`developers.facebook.com` returns **HTTP 200 with an empty navigation shell** for URLs that don't exist, and `help.instagram.com` / `facebook.com/business/help` redirect freely. `curl` and `mint broken-links` see success either way.

**Never guess a Meta URL from its topic, and never trust a curl 200 for one.** `WebFetch` it and confirm real content:

```
WebFetch <url> "Does this page have real documentation content, or is it an empty
placeholder / page not found? Summarise what it actually covers."
```

```bash
# every Meta link currently on the site
grep -rnoE --include="*.mdx" 'https?://[^ )"]*(facebook|instagram|meta)\.com[^ )"]*' .
```

Link the **final** URL, not one that redirects. Once confirmed, add it to the verified link set in `comentify-docs` §6 with the date. If a page can't be confirmed, state the rule without a link.

---

## Reporting

Group findings by section (§1–§6). For §2, report the **count of files affected**, not just the first hit. For §6, report each Meta link as confirmed-live, confirmed-dead, or not-yet-checked — never treat "not yet checked" as "fine".
