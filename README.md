# NOMAD AI LAB

Cloudflare Workers Static Assets deployment of the LP previously hosted at
https://ai-web-creator.netlify.app/.

Source baseline: `diamond0307-ctrl/AI_creator` commit
`81ce39dba6d6b04276ffbd97cc8fbb807dbf8c81`.
The original repository, Netlify site, and Cloudflare `ai-creator` project are independent and unchanged.

## Local build

```sh
npm ci
npm test
npm run build
npm run preview
```

Vite builds React and the prerender script generates the initial HTML.
`public/` and `output/` preserve the original published static asset paths.
Only `dist/` is uploaded. There is no Worker script, server function, database,
or runtime secret. Unknown paths return 404; this LP has no client-side path router.

## Cloudflare GitHub integration

- Repository: `diamond0307-ctrl/nomad-ai-lab`
- Worker name: `nomad-ai-lab`
- Production branch: `main`
- Root directory: `/`
- Build command: `npm test && npm run build`
- Deploy command: `npx wrangler deploy`
- Build/runtime variables: none required
- Public URL: https://nomad-ai-lab.art-4-being0801.workers.dev/

Cloudflare Workers Builds installs dependencies from the lockfile and deploys
when commits are pushed to this repository's `main` branch. Configure the GitHub
connection in Cloudflare; do not store a Cloudflare API token in this repository.
Wrangler is pinned in the lockfile. `.env*`, `.dev.vars*`, `.wrangler/`, build
output, and dependency directories are ignored.

## Preserved attribution

All seven LINE CTAs use the existing centralized handler:

| Landing parameters | Route | Destination |
| --- | --- | --- |
| `utm_medium=paid_social` (highest priority) | `paid_social` | `https://lin.ee/ytZkQYq` |
| `utm_source=instagram&utm_medium=social` | `instagram_social` | `https://lin.ee/zJ3C7o9` |
| No UTM, `fbclid` alone, or other UTM | `other_or_unknown` | `https://lin.ee/zJ3C7o9` |

GA4 `G-BFVWD1W4SZ` sends `page_view` and `line_click`.
Meta Pixel `1040951598718706` sends `PageView`, `Lead`, and `LineClick`.
These browser-visible measurement identifiers are not secrets.
CTA events measure outbound clicks; they do not prove completed LINE friend additions.
