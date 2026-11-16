# DeenHub

Context for Claude. Read this before doing anything in this repo.

## About the owner

- The owner is a **vibe coder, not a programmer**. Keep explanations short, friendly and in plain language. No jargon walls, no long lists of options. Give one clear recommendation.
- When the owner needs to do something in a dashboard (Cloudflare, GitHub), give simple numbered steps, and say what they should see when it works.
- The owner often shares screenshots. Read them carefully before answering.
- Do the technical work yourself (code, commits, pull requests) rather than asking the owner to run commands.

## What this is

DeenHub is an Islamic website. The idea and features are still being decided with the owner. Right now the site is just a placeholder landing page. When the owner describes the idea, build it here.

## How the site is built and hosted

- **Plain static site**: HTML, CSS and JavaScript in the `public/` folder. No framework and no build step (yet).
  - `public/index.html` is the home page.
  - `public/404.html` is the "page not found" page.
- **Hosting**: Cloudflare Workers, serving `public/` as static assets. The Worker is named `deenhub`.
- **Config**: `wrangler.jsonc`. It sets the assets folder, turns on the `workers.dev` production URL and turns on preview URLs.
- **Cloudflare builds are connected to this GitHub repo**:
  - **Production**: branch `main`, deploy command `npx wrangler deploy`. Every change to `main` goes live.
  - **Preview**: every other branch, deploy command `npx wrangler versions upload`. Each push gets its own preview link, which the owner finds under **Deployments** in the Cloudflare dashboard.
- If a framework (React, Astro, etc.) is ever added, add a build command in Cloudflare and point `assets.directory` in `wrangler.jsonc` at the build output folder (for example `./dist`).

## How we work

1. Make changes on a **separate branch**, never directly on `main`.
2. Push the branch. Cloudflare builds a preview link.
3. Tell the owner where to find the preview, and what changed, in a few lines.
4. The owner checks the preview. They either ask for changes or say "merge".
5. Only merge into `main` when the owner says so. Open a pull request and merge it (squash).
6. After a merge, start the next piece of work from the latest `main` so pull requests don't conflict.

Before pushing, check the site still deploys:

```bash
npx wrangler deploy --dry-run
```

It should say it read the files from the `public` assets directory, with no errors.

## Design notes

- The current page uses a calm green accent (`#1f6f50` light, `#5cc796` dark) on a warm off-white or near-black background, and follows the visitor's light or dark mode.
- Pages must work well on phones.
- Treat Islamic content with care: Quran text, hadith and translations must come from reliable, properly attributed sources. Never invent or paraphrase them as if they were exact quotes.

## History

- The first Cloudflare deploys failed with "Could not detect a directory containing static files" because the repo only had a README. Fixed by adding `wrangler.jsonc` and the `public/` folder.
- Production and preview URLs are set up and working. The placeholder page is live.
