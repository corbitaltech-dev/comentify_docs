---
name: docs-fact-check
description: How to verify a documentation claim against the real Comentify product before publishing it — locating the feature in the product source or the live app, confirming exact UI button and status labels, checking plan gating and limits, and checking Meta/Instagram rules against Meta's own pages. Activate when writing any factual claim about how the product behaves, when a page mentions a button/screen/limit, when auditing an existing page for accuracy, or when the user asks whether a documented behaviour is real.
---

# Fact-checking a docs claim

Every behavioural claim in the docs must be traceable to the product. A page that describes a button that doesn't exist is worse than a missing page — it burns the trust the docs are there to build.

⚠️ **The current Comentify pages are not evidence.** They were generated from a product brief, not written against the running app. Labels such as **Settings → Connected Accounts**, **New Rule**, **Save & Activate**, **Activity** tab, and terms such as "90 days" retention are unverified. Never confirm a claim by finding it on another page.

---

## Where the truth lives

**Product source: not yet configured.** It is not on the docs machine. Before verifying anything, ask the user for one of:

1. the product repo path (then record it here, with the stack and the folders that hold UI strings), or
2. a staging or demo login (then verify by using the app and taking screenshots), or
3. screenshots of the exact screen from someone who can see it.

Once the source is known, replace this section with the path, the stack, and the grep recipe for UI labels (e.g. `grep -rn "Save & Activate" resources/js --include="*.vue"`), and remove the corresponding row from `comentify-docs` §0.

**Pricing and limits:** `comentify.io/pricing` is the public source; `account/plans.mdx` must never contradict it. Any number goes on the plans page only (`comentify-docs` §2).

**Meta rules:** Meta's own help-centre and developer pages, fetched and read — see `comentify-docs` §6.

## What must be verified before it ships

- **Every UI label** — button text, menu item, page name, tab, field label.
- **Every status value** — e.g. `Active`, `Paused`, `Connected`, `Disconnected`. Case matters; the docs show what the screen shows.
- **Every navigation path** — "Automation → Comment Replies → New Rule" must match the real sidebar.
- **Every plan gate** — is this feature really on every plan?
- **Every limit, price, retention period, or refund term** — and these belong only in `account/plans.mdx`.
- **Every Meta rule** — account types, messaging window, private-reply rules, permissions requested. Meta's page decides, not memory.

## How to check without source access

- **Screenshots from the author** — read the labels, but treat them as candidates: vision misreads text. If two screenshots disagree, ask.
- **The live app** — if the user gives you a login, verify by doing the task. Note the date checked.
- **The marketing site** — `WebFetch comentify.io` pages for plan names and public claims. Marketing copy can lag the app, so it confirms naming, not behaviour.

## When you can't verify

State it rather than guessing. Leave the claim out, or add a `<Note>` caveat, and flag it to the user. Never soften an unverified claim into vague language to make it feel safe — vague and wrong is still wrong.

## Known traps

- **Generated pages look authoritative.** Confident, specific wording ("Click **Confirm Upgrade**") is not evidence the button exists.
- **Meta changes rules often.** Messaging windows, private-reply rules and permission names have all moved over the years. Re-check against Meta rather than trusting a claim written months ago.
- **Plans page vs. pricing page.** If `account/plans.mdx` disagrees with `comentify.io/pricing`, the pricing page wins and the docs page needs fixing — say so rather than quietly matching the stale page.
