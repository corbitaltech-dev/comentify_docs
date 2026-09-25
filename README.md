# Comentify Docs

Source for the documentation site of [Comentify](https://comentify.io/), a hosted Instagram and Facebook engagement-automation service by Corbital Technologies LLP.

Comentify helps businesses turn social engagement into conversations and leads. Depending on the plan, it includes:

- Connected Instagram professional accounts and Facebook Pages (via Meta's authorization flow)
- Comment-to-message automation
- Automated message and comment replies
- Workflows
- A shared inbox
- Contacts and lead capture
- Analytics
- Team access
- AI-assisted features

The docs are built with [Mintlify](https://mintlify.com/docs). Pages are written in MDX, and site navigation lives in `docs.json`.

## Local development

Install the Mintlify CLI:

```bash
npm i -g mint
```

From the repository root (where `docs.json` lives), start the preview server:

```bash
mint dev
```

Open `http://localhost:3000` to view the site. Pages reload as you save.

Before you open a pull request, check for broken links:

```bash
mint broken-links
```

## Writing guidelines

- **Write for the customer.** Readers are business owners and social media teams, not developers. Use plain language and name UI elements exactly as they appear in the app.
- **One task per page.** Start with what the reader will achieve, list prerequisites, give numbered steps, then show how to confirm it worked.
- **Screenshots** go in `images/`, grouped by section. Every image needs descriptive alt text.
- **Mark paid features** with the plan they require.
- **Follow Meta's rules.** Where a feature depends on a Meta platform policy (for example, the 24-hour messaging window or permission scopes), link to Meta's official documentation rather than paraphrasing it.
- **Don't invent product behavior.** If you're unsure about a label, limit, or behavior, check it in the product before you publish.

## Adding a page

1. Create an `.mdx` file in the right section folder, with `title` and `description` frontmatter.
2. Add the page path (without the extension) to the `navigation` section of `docs.json`.
3. Preview it with `mint dev`, then run `mint broken-links`.

## Publishing

The Mintlify GitHub app deploys the site. Changes merged into the default branch go to production automatically. Use pull requests for all changes so someone else can review them first.

## Troubleshooting

- **The preview won't start:** run `mint update` to get the latest CLI.
- **A page returns 404:** make sure you're running `mint dev` in the folder that contains `docs.json`, and that the page is listed in `docs.json`.

## Support

- Product: [comentify.io](https://comentify.io/)
- Mintlify reference: [mintlify.com/docs](https://mintlify.com/docs)

© Corbital Technologies LLP. All rights reserved.
