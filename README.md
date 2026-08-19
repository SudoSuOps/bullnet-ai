# bullnet.ai — holding page

The compute sub-brand of BullPrint Net, while the real platform page is built.
Static, no build step, no framework, **no JavaScript at all**. Deploys to
Cloudflare Pages from the repo root.

```
.
├── index.html          the page
├── styles.css          every style
├── fonts/              Inter + JetBrains Mono, self-hosted, woff2
├── assets/             favicons + the shared B-glyph mark
├── _headers            security + cache headers
├── favicon.ico         real multi-size icon (16/32/48)
├── site.webmanifest
├── robots.txt
└── sitemap.xml
```

## Cloudflare Pages settings

| | |
|---|---|
| build command | *(none)* |
| build output directory | `/` |
| framework preset | None |
| production branch | `main` |

Custom domain: **`bullnet.ai`**. This is the page the three `bullnet.ai` links
on bullprintnet.com are pointing at — until this deploys, those links are dead.

## Built from

`BullNet AI Holding Page.dc.html`, design project
`9dd423de-c1da-4abe-b2e6-2931610f721f`. Every string was diffed against the
design and all of it carried over.

Two things in the source are design-tool artefacts rather than markup and were
translated rather than copied:

- **`style-hover="…"` attributes.** Not real HTML — a `.dc` runtime convention.
  Rewritten as actual `:hover` rules.
- **The Google Fonts `<link>`.** Replaced with the same self-hosted woff2 files
  that serve bullprintnet.com, for the same reason: a page selling private
  infrastructure should not make a third-party request to render its own name,
  and self-hosting is what lets `_headers` carry a CSP with no external origins.

## What this repo used to hold

A copy of the bullprintnet.com landing page, pushed here before
`bullprintnet-app` existed. That has been removed — the landing page lives in
`SudoSuOps/bullprintnet-app` and is deployed at bullprintnet.com. This repo is
the bullnet.ai holding page and nothing else.

## Brand position

`BRAND_KIT.md` is explicit that bullnet.ai is **subordinate**: same tokens, same
type, **no separate mark**, and a footer credit to the parent. So:

- The header carries the `BULLNET.AI` wordmark as type, not a logo, with `.AI`
  in `#6E6A83` per the kit's lockup spec.
- The parent credit — "A BullPrint Net Platform ↗" — links to bullprintnet.com.
- The **favicon is the master brand's B glyph**, not a new mark. "No separate
  mark" is the rule, so the sub-brand borrows rather than inventing one. If the
  two sites ever need to be told apart in a tab strip, that is a brand-owner
  decision, not a build one.

## Notes on the build

**`script-src 'none'`.** There is no JavaScript on this page, so the CSP closes
the directive outright rather than allowing `'self'`. If anything scripted is
ever added here, that header has to change deliberately.

**Both animations stop under `prefers-reduced-motion`.** The status dot pulses
and the caret blinks — a blinking cursor is close to the canonical example of
what that setting exists to suppress. Both hold at full opacity instead.

## Open

- This is a holding page. The real compute platform page is not designed yet.
- `og:image` is not set — there is no banner for this sub-brand, and pointing it
  at the BullPrint Net banner would misrepresent the link in a share card.
  Worth commissioning one if bullnet.ai gets shared much.
