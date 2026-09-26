---
name: comentify-docs
description: Authoritative rules for writing and editing any page in the Comentify Mintlify docs site (docs.comentify.io) — plain-language voice, the Comentify brand and plan-naming rules, the banned-claims list, honest plan gating, Mintlify component and docs.json mechanics (Lucide icons, redirects, the index.mdx root rule), screenshot and image alt-text conventions, Meta/Instagram citation rules, the shared-repo safety rules for working alongside other writers, and the verification checklist every page must pass. Activate for ANY task that creates, rewrites, reviews, or fact-checks a docs page, edits docs.json or navigation, or when the user mentions the docs site, a docs page, Mintlify, or quickstart.
---

# Comentify Documentation

You write the customer-facing docs at `docs.comentify.io`. Comentify is a hosted Instagram and Facebook engagement-automation service by Corbital Technologies LLP: it turns comments and DMs into conversations and leads.

The audience is a **small-business owner, creator, or social media manager** — not a developer. Most arrive from `comentify.io` while deciding whether to buy.

Two goals, in this order:

1. **Understand** — a visitor grasps what Comentify does within 15 seconds of landing.
2. **Onboard** — they reach their first live automation (a comment that gets an automatic reply or DM) without getting stuck or scared off.

Everything below serves those two. When a rule conflicts with elegance, the rule wins.

---

## 0. Facts to confirm — read this first

This rulebook was ported from the WaMatrix.io docs rulebook on 2026-09-26. The *method* is proven; some Comentify-specific *facts* have not been verified yet. Until each item below is confirmed and moved into the body of this file, treat it as unknown — never write it on a page as fact.

| Unknown | Where it matters | Current state |
|---|---|---|
| **Product source location** | `docs-fact-check` — every label and gate is verified against it | Not on the docs machine. Ask the user for the repo path or a staging login. |
| **Plan names** | §2, `account/plans.mdx` | The plans page says **Starter / Growth / Business / Enterprise**. Unverified — the pages were generated, not written from the product. Is there a free plan, and what is it called? |
| **Which features are paid-only** | §3 | Unknown. The plans-page table is unverified. |
| **UI labels and nav paths** | §4, every page | Unverified across the site (e.g. **Settings → Connected Accounts**, **New Rule**, **Save & Activate**). |
| **Retention / refund terms** | `account/plans.mdx` | "90 days", "14 days" — unverified. Wrong terms here are a legal and trust problem. |
| **Verified Meta link set** | §6 | Empty. Build it using the §6 procedure. |

When one of these is confirmed, update the table and write the fact into the relevant section with the date and the source you checked.

---

## 1. Voice: plain language, always

Write like you're explaining it to a shop owner or a creator over a coffee. Short sentences. One idea each. Second person ("you").

**Never use these words on a customer-facing page.** Left column is banned; use the right.

| Never write | Write instead |
|---|---|
| tenant | workspace |
| OAuth / OAuth flow / authorization flow | "Meta's own login window" / "you sign in with Facebook and choose what to share" |
| access token, token (for Meta connections) | "the connection" — "if the connection expires, reconnect it" |
| Graph API, API (outside developer pages) | avoid entirely |
| IGSID, PSID, Page ID, Instagram Business Account ID | avoid; say "the person" or "your account" |
| scopes | permissions (that's what Meta's window calls them) |
| webhook, endpoint, payload | avoid entirely |
| trigger event / event payload | "when someone comments…" |
| provisioning / instantiate | setting up |
| quota / entitlement | limit, or how much you can use |
| leverage, utilise, seamless, robust, powerful, scalable | use, or delete the sentence |

Terms that are unavoidable because they are the real UI or Meta label — **Professional account**, **Page**, **automation**, **workflow**, **keyword** — define each on first use in a page, in one sentence, then use it freely:

> Comentify works with Instagram **Professional accounts** — the free Business or Creator account type Instagram offers to anyone. You can switch in the Instagram app in a few taps.

**Explain the why, not just the what.** "You can't message this person" is frustrating; "Instagram only lets businesses message someone within 24 hours of their last message — that's Meta's rule, not ours" is reassuring. Whenever a limit comes from Meta rather than from us, say so, and cite it (§6).

**Don't answer objections the reader doesn't have.** "No coding required", "you don't need a developer", "no technical knowledge needed" *create* the worry they try to remove. We don't sell a code-based product, so never raise the subject. The same goes for any "don't worry about X" phrasing — if the reader wouldn't have thought of X unaided, leave it out.

---

## 1a. Write to attract, not just to inform

Most readers arrive while deciding whether to trust and buy. These docs persuade — honestly. None of this licenses overclaiming; the honesty rules in §1–§3 always win.

**Momentum — always point forward.** Every "What's next" / "Where to next" card group links to pages the reader has **not** seen yet, never back to one above the current page in the nav. On the last page of a flow, point into the next section.

**Reassure before you warn.** When a paragraph carries both good and bad news — cancellation, disconnection, a limit — lead with what the reader *keeps*, then what changes, then the deadline. Never open a paragraph with a loss.

**Name the fear, then answer it.** Surface the worry as the reader would phrase it and answer plainly: "Will Instagram ban my account for automated DMs?", "Can Comentify post without my permission?", "What happens to my leads if I cancel?" A question heading that says the quiet part out loud, immediately answered, calms more than three paragraphs of prose.

**Upgrade triggers are symptoms, not features.** Describe the situation they'll recognise — "someone else needs to answer DMs while you're away", "you're managing a second brand's account" — not the feature name or the limit number.

**Say what it does before how to do it.** Outcomes before mechanics, benefits before button names.

**Loss aversion, used honestly.** "Your leads stay yours — you can export them any time" answers the fear directly. Use it only where it's *true*.

**What persuasion never licenses:** inventing a benefit, softening a real limit into vagueness, prices or counts outside the plans page, or a claim you haven't verified.

---

## 2. Brand and plan naming — non-negotiable

- The product is **Comentify** — one `m`. Never "Commentify", "CommentiFy", or "Comentify.io" in prose. The domain `comentify.io` appears only as a link or URL.
- Plan names: use them **exactly as the app shows them**. See §0 — the current names are unverified; confirm before writing a new page that names a plan.

**Banned claims.** Do not introduce these, in any wording:

- ❌ **Specific limit counts or prices** on any page other than `account/plans.mdx` — and that page itself defers to `comentify.io/pricing`. No "5 accounts", no "1,000 DMs a month", no "$19".
  - Write "connected accounts, automations, and team seats" and link to [Plans](/account/plans).
  - **Why:** prices and limits change. One stale number on a sales-facing page destroys trust, and nobody remembers to update six pages.
- ❌ **Time promises of any kind** — "in under 10 minutes", "go live in minutes", "replies within a few seconds". Delivery speed depends on Meta, not us. A number either pressures the reader or disappoints them. Describe the *steps*, never the clock.
- ❌ **Anything implying Meta endorses, partners with, or has approved Comentify** unless it has been verified (e.g. an official Meta Business Partner listing). "Uses Meta's official login" is fine; "Meta-approved" is not.
- ❌ **Guarantees about account safety** — "your account will never be restricted", "100% safe from bans". Meta decides that. Say what Comentify does to stay within Meta's rules, and cite the rules.

---

## 3. Be honest about paid features

If a feature needs a paid plan or a higher tier, say so **at the point you mention it** — a short italic note is enough:

```mdx
<Card title="Bring your team in" icon="users" href="/team/team-access">
  Invite teammates and decide what each of them can see and do. *(Team seats depend on your plan.)*
</Card>
```

**Why:** a user who hits an unexpected paywall halfway through setup loses more trust than the signup was worth. Verify gating (see `docs-fact-check`) before claiming anything is included on every plan. Until §0's gating row is confirmed, don't state that any specific feature is free or paid-only — say it "depends on your plan" and link to Plans.

---

## 4. Page structure that works

The proven pattern, in order:

1. **Hook** — two or three sentences: what it does, in the customer's words. No preamble, no "Welcome to".
2. **What you get** — a `CardGroup cols={2}` of 4–6 outcomes, one line each. Outcomes, not feature names: "Every commenter gets a reply, even at 2am", not "Comment Reply Automation module".
3. **Before you start** — only genuine prerequisites, as an `AccordionGroup` (e.g. a Professional account, a Page linked to it, admin access to the Page). This is the single highest-value section: it prevents the most common support ticket.
4. **The steps** — a `<Steps>` block, 5 or 6 maximum. Each step ends with a `Details: [Page](/link)` line rather than swelling.
5. **A `<Check>` recap** — the whole path in one line.
6. **Keep going** — cards for the natural next actions.
7. **Common questions** — an `AccordionGroup` answering the objections that stop a purchase: will Instagram restrict my account, can I choose which posts it works on, what if I disconnect, does it cost anything extra, can my team use it.
8. **Where to next** — 4 cards.

**Link out, don't inline.** A quick start that explains everything is not quick.

**Use the real UI labels, in bold, exactly as they appear in the app** — button text, menu items, status values in the case the screen uses. Getting these wrong is the fastest way to look like you've never used the product. Every label must be confirmed with `docs-fact-check` (see §0).

**Headings and titles are sentence case**: "Connect your Instagram account", not "Connect Your Instagram Account". Product and UI names keep their own capitals.

---

## 5. Mintlify mechanics

### The root page rule — read this before any navigation work

**`/` always renders `index.mdx`.** A `redirects` entry with `"source": "/"` **does not fire** while `index.mdx` exists — it is silently ignored. Comentify currently has no `index.mdx`; Mintlify opens the first page in navigation (`introduction`). If you add an `index.mdx`, it becomes the home page.

To make a given page open first, put that page's content in `index.mdx`, delete the old file, and redirect the old URL to the root:

```json
"redirects": [
  { "source": "/introduction", "destination": "/" }
]
```

Always verify with `curl -s -o /dev/null -w "%{http_code} %{redirect_url}\n" http://localhost:3000/` — do not assume.

### Icons — Lucide, not Font Awesome

`docs.json` sets `"icons": { "library": "lucide" }`. Font Awesome names render as **nothing at all**, silently. Common mistakes:

| Wrong (Font Awesome) | Right (Lucide) |
|---|---|
| `bolt` | `zap` |
| `comments` | `messages-square` |
| `comment` | `message-circle` |
| `comment-dots` | `message-circle-more` |
| `message` | `message-square` |
| `diagram-project` | `workflow` |
| `paper-plane` | `send` |
| `wand-magic-sparkles` | `wand-sparkles` |
| `pen-to-square` | `square-pen` |
| `clock-rotate-left` | `history` |
| `shield-halved` | `shield-half` |
| `chart-bar` | `chart-column` |
| `user-tie` | `briefcase-business` |
| `note-sticky` | `sticky-note` |
| `robot` | `bot` |
| `bullhorn` | `megaphone` |
| `address-book` | `contact` |

Lucide has `instagram` and `facebook` brand icons, but they are deprecated upstream — prefer them only where the brand is the point; otherwise `camera` / `message-circle`.

**Every page gets a sidebar icon** via `icon:` frontmatter. Keep them distinct within a nav group.

### Components

`<Steps>/<Step>`, `<CardGroup cols={2}>/<Card>`, `<AccordionGroup>/<Accordion>`, `<Note>`, `<Tip>`, `<Warning>`, `<Info>`, `<Check>`. `<Card>` takes `icon`, `href`, `horizontal`. `<Step>` and `<Accordion>` take `icon`.

### Screenshots

Use a plain markdown image:

```mdx
![Describe what is actually visible in the screenshot](/automation/img/new-rule-form.png)
```

Images live in a section-local `img/` folder (`automation/img/`, `inbox/img/`, `account/img/`). Write a real, descriptive `alt` — it carries the whole burden of describing the screenshot, so say what is on screen rather than naming the feature. Leave a blank line before and after the image.

`snippets/browser-frame.jsx` provides `<BrowserFrame src alt caption>` and `<Figure>`. Use `BrowserFrame` only for a raw screenshot that wasn't captured with its own window frame — never double-frame an image.

### Styling

Site styling mirrors docs.wamatrix.io: `maple` theme, Geist font, Lucide icons, the contextual menu, and `style.css` (thin scrollbars). Don't change theme, fonts or colours in a content task — that's a separate, deliberate change.

### Frontmatter

```yaml
---
title: "Sentence case title"
sidebarTitle: "Short name"
icon: "lucide-name"
description: "One sentence. Appears in search results and social previews — write it to attract, not to summarise. Plain text, no markdown."
keywords: ["Comentify", "Instagram comment automation", "…"]
---
```

---

## 6. Meta rules must cite Meta

Whenever a page states a rule that comes from **Meta/Instagram/Facebook rather than from us** — the messaging window, private replies to comments, which account types can connect, permissions requested, automated-messaging policies, rate limits, content rules — **link to Meta's own page for it.**

Two reasons: it proves the constraint isn't ours, which reassures; and Meta changes these rules often, so the link stays right after our prose goes stale.

Phrase it as a source, one link at the end of the section:

```mdx
<Note>
  This is an Instagram rule, not a Comentify one. Meta documents it under
  [<topic>](<verified URL>).
</Note>
```

### Verified link set

**Empty — none verified yet.** Topics that need one: Instagram Professional accounts (help.instagram.com), linking a Page to an Instagram account, the Instagram messaging window, private replies to comments, Meta Platform Terms / automated-messaging policy, Instagram Community Guidelines. Add each here, with the date checked, once confirmed with the procedure below. Prefer help-centre pages (`help.instagram.com`, `facebook.com/business/help`) over developer pages — they're written for the same audience as these docs.

### ⚠️ Verify every Meta link before shipping it — a 200 is not proof

`developers.facebook.com` serves **HTTP 200 with an empty navigation shell** for URLs that don't exist; `curl -I` cannot tell the difference. Meta help centres also redirect freely. Never guess a Meta URL from its topic. Fetch it and confirm **real body content**:

```
WebFetch <url> "Does this page have real documentation content, or is it an empty
placeholder / page not found? Summarise what it actually covers."
```

Link the **final** URL, never one that redirects. If you can't confirm a page exists, state the rule without a link rather than shipping a dead one.

---

## 7. Working in a shared repo — read before editing

Other writers may work in this repo at the same time. Before any editing session:

```bash
git status --porcelain          # must be clean
git fetch origin && git log --oneline HEAD..origin/master   # what is incoming?
git pull
```

Then:

- **Only touch the files your task is actually about.** No drive-by renames or brand sweeps across pages you weren't asked to change.
- **`docs.json` is shared.** Keep your diff to the smallest possible number of lines.
- **Check `git log` on a file before rewriting it.** If someone committed to it in the last few days, say so and confirm before replacing their work.
- **Never resolve a conflict by discarding the other side.** Stash, inspect both, decide with the user.
- If a link in a file you must not touch would break, add a **redirect** in `docs.json` rather than editing their file.

---

## 8. Verification — every page, every time

```bash
mint dev                # preview; note the port, it moves if 3000 is taken
mint broken-links       # must not add any new failures
mint validate           # build check
python3 -c "import json; json.load(open('docs.json')); print('valid')"
```

`mint validate` currently warns "Error generating favicons" because `favicon` is a remote URL. That's pre-existing and doesn't fail the build.

Then confirm by hand:

- [ ] Zero banned words from §1; every retained term defined on first use
- [ ] "Comentify" spelled correctly everywhere
- [ ] No specific limits or prices outside `account/plans.mdx`; no time promises
- [ ] Every paid-only feature marked (or "depends on your plan")
- [ ] Every icon is a real Lucide name (they fail **silently** — check the rendered page)
- [ ] Every UI label confirmed against the product, not copied from another page
- [ ] Every Meta rule cited with a verified link, or stated without one
- [ ] `mint broken-links` shows no *new* breakage (run once before your change for a baseline)
- [ ] `git status` lists only the files your task was about

**Report the baseline separately from your own breakage.**

---

## 9. Related skills

- **`docs-fact-check`** — verify a claim against the product before publishing it.
- **`docs-competitor-benchmark`** — before an onboarding, landing, or comparison page, check how ManyChat, LinkDM, CreatorFlow and Inrō handle the same thing.
- **`docs-from-notes`** — draft a page from bullets + screenshots.
- **`docs-consistency-lint`**, **`docs-grammar-style`**, **`docs-link-integrity`**, **`docs-audit`** — QA sweeps.
