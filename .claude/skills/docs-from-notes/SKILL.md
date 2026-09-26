---
name: docs-from-notes
description: Turns a short, point-by-point feature description plus screenshots into a complete, on-brand Comentify docs page. Reads the images to see the real UI (labels, buttons, states), reads the author's terse bullets, then expands them into a full MDX page that follows the house voice and the proven page structure — hook, what you get, before you start, steps, check, keep going, common questions, where next — with each screenshot placed as a plain markdown image with descriptive alt text, plan gates marked, Meta rules cited, and every fact flagged for verification. Expansion means wording, flow, and structure only: it never invents a label, limit, or behaviour that isn't in the notes, the image, or the verified product. Activate when the user provides feature notes and/or screenshots and wants them written up, says 'draft a page from these bullets', or hands over a filled intake template.
---

# Docs from notes + screenshots

The author gives you a little; you produce a complete page. **Your job is to expand wording, flow, and structure — never to invent facts.** A label, limit, or behaviour that isn't in the notes, visible in the image, or confirmed in the product does not go on the page.

**Read `comentify-docs` first** — voice, banned words, brand, Mintlify mechanics, Meta-citation rules, and the page structure you build to. Verify facts with `docs-fact-check`; check the finished page with `docs-reviewer`.

For Comentify, screenshots and author notes are currently the **main source of truth** for UI labels, because the product source isn't available on the docs machine (`comentify-docs` §0). That makes Step 1 more important, not less.

---

## What you receive

Ideally the author fills `INTAKE-TEMPLATE.md` (next to this skill). If they send loose bullets, infer the mapping and confirm. Per feature you need:

- the feature name **as the app shows it**,
- one line on what it does, in customer words,
- the steps in order, with exact button labels,
- the screenshots, each with a one-line "this shows…" and which step it belongs to,
- the plan gate, prerequisites, and gotchas.

## Step 1 — Read the screenshots

For each image record: which screen it is, the exact visible labels and button text, any status values (`Active`, `Paused`, `Connected`), and what a reader should notice.

⚠️ **Vision can misread text.** A label read off an image is a *candidate*. If the notes and the image disagree, ask the author which is current — don't pick silently.

## Step 2 — Verify the facts

- **Labels & nav paths** — screenshot + notes agree, or confirmed via `docs-fact-check`.
- **Plan gate** — never guess. If unknown, write "depends on your plan" and link to Plans.
- **Limits & prices** — only on `account/plans.mdx`; link there.
- **Meta rules** — account types, messaging window, private replies: cite Meta's page (`comentify-docs` §6), or state without a link if none is verified.

Anything you can't verify: draft around it and **flag it to the author**. Never soften an unverified claim into vague wording to make it feel safe.

## Step 3 — Choose the structure

Map the notes to the proven pattern (`comentify-docs` §4). **Use only the sections that fit.**

| Section | Build it from | Skip when |
| --- | --- | --- |
| **Hook** (2–3 sentences) | the one-line "what it does" | never |
| **What you get** (`CardGroup`) | multiple distinct outcomes | a single-purpose feature |
| **Before you start** (`AccordionGroup`) | the prerequisites bullet | no real prerequisites |
| **Steps** (`<Steps>`, 5–6 max) | the ordered step bullets | no procedure |
| **`<Check>` recap** | the whole path in one line | a reference/settings page |
| **Keep going** (cards) | related pages | nothing natural to point to |
| **Common questions** (`AccordionGroup`) | the gotchas / "why can't I…" | no known objections |
| **What's next** (cards) | related pages, forward only | — |

Momentum rule: "Keep going" and "What's next" point to pages the reader **hasn't** seen yet (`comentify-docs` §1a).

## Step 4 — Write the prose

Plain, short sentences. Outcomes before mechanics; benefit before button name. Exact UI labels in **bold**. Define **Professional account**, **automation**, **workflow** on first use. Mark plan gates where you mention them. No "no coding required", no time promises.

## Step 5 — Place the screenshots

- Copy each image into the **section-local `img/` folder** (`automation/img/`, `inbox/img/`) with a descriptive name (`dm-rule-keyword-field.png`, not `image3.png`).
- Place it as a plain markdown image beside the step it illustrates:
  ```mdx
  ![Describe exactly what is on screen](/automation/img/dm-rule-keyword-field.png)
  ```
- The `alt` carries the full description: fields, their values, the state of any toggle.
- If the screenshot is a raw crop without a window frame, `<BrowserFrame src="…" alt="…" />` from `snippets/browser-frame.jsx` is available — never on an already-framed image.
- One image per meaningful step; don't front-load images at the top.

## Step 6 — Frontmatter

```yaml
---
title: "Sentence case title"
sidebarTitle: "Short name"
icon: "lucide-name"     # Lucide only; they fail silently
description: "One sentence, written to attract. Plain text, no **bold**."
keywords: ["Comentify", "…"]
---
```

Add the page to `docs.json` navigation in the right group, with the smallest possible diff.

## Step 7 — Gaps: ask, don't invent

Ask **only** when a gap blocks the page — an unknown prerequisite, an unclear plan gate, a step whose outcome you can't tell. Otherwise draft and state any assumption inline. Deliver everything that isn't blocked first; ask about the rest in one batch.

## Step 8 — Review before it's "done"

- Show the author the **rendered copy**, not a diff or a file path.
- Run `docs-reviewer` on the new page.
- `mint dev`, `mint broken-links`, and **confirm icons rendered** (Lucide fails silently).

---

## Worked example (compact)

**Author's input:**
> Feature: Comment-to-DM. What: when someone comments a keyword, send them a DM with a link. Plan: not sure. Steps: 1) Automation → DM Automation → **Create Automation** 2) pick a post, type keyword in **Keywords** 3) write the DM in **Message** 4) **Save**. Screenshot: `dm-keyword.png` = the keyword field (step 2). Gotcha: Instagram only allows one private reply per comment.

**Draft output (excerpt):**
```mdx
---
title: "Send a DM when someone comments"
sidebarTitle: "DM Automation"
icon: "send"
description: "Turn every comment on your posts into a private conversation — automatically, with the link or offer they asked for."
keywords: ["Comentify", "comment to DM", "Instagram DM automation"]
---

When someone comments a keyword on your post, Comentify sends them a private message with whatever you promised — a link, a discount code, a price list. *(Availability depends on your plan — see [Plans](/account/plans).)*

<Steps>
  <Step title="Start a new automation">
    Go to **Automation → DM Automation** and click **Create Automation**.
  </Step>
  <Step title="Choose the post and keyword">
    Pick the post, then type the word people will comment in **Keywords**.

    ![The Keywords field with the word LINK entered, below a selected Instagram post thumbnail](/automation/img/dm-keyword.png)
  </Step>
  <Step title="Write the message">
    In **Message**, write what the person receives. Click **Save**.
  </Step>
</Steps>

<Note>
  Instagram lets a business send one private reply to each comment. That's Meta's rule, not ours.
</Note>
```

Notice: the unknown plan gate became "depends on your plan", labels are bold and exact from the notes, the image sits beside its step with a descriptive alt, and the gotcha became a `<Note>` framed as Meta's rule. Before shipping, the labels get confirmed and the Meta rule gets a verified citation — or ships without a link.
