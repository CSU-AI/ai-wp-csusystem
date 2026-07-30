# ai.csusystem.edu build context

Campus AI site for the CSU System. Owner: David Edwards, AI Strategist, CSU System.
Build locally first, then migrate to production.

Sister site: ai.colostate.edu (CSU Fort Collins). Same build method, same class
names, different palette. Do not carry Fort Collins colors into this repo.

## Constraints

- Theme is provided by CSU Web Services and was built for Elementor. **Do not edit theme files.**
- All styling lives in one file, `docs/aicsu-design-system.css`, served via GitHub
  Pages and linked from the theme with a single `<link rel="stylesheet">`. Every
  class is prefixed `.aicsu-` so nothing collides with the theme. Edits to this
  file go live on push, no manual re-paste needed.
- All page layout is core Gutenberg blocks. No Elementor authoring. No page builders.
- Pages are built by applying design system classes in each block's
  **Additional CSS class** field. Never write inline styles.
- Accessibility target is WCAG 2.1 AA.

## Theme facts

Established by inspection, 07/2026. The theme is `csu-theme`; body carries
`wp-theme-csu-theme`. These change how CSS must be written, so check them
before adding a selector.

- **The theme rewrites button markup.** Core's `wp-block-button__link` is
  replaced with `btn btn__md wp-element-button`. Every button selector must
  name both, or it matches nothing on the rendered page.
- **The theme strips `wp-block-column`** off Column blocks. Card rules key off
  `.aicsu-card`, never the core class.
- **Group blocks render an inner `.wp-block-group__inner-container`.** A child
  selector like `.aicsu-inner > .wp-block-buttons` matches nothing; the buttons
  are grandchildren.
- **No `page-id-*` body class is emitted.** Page-scoped rules use WordPress's
  own body classes (`.home`, `.page`) instead.
- **The theme zeroes block margins.** Consecutive blocks meet flush. Any
  spacing between blocks comes from the design system.
- **The footer is painted Pueblo Blue `#1F2759`**, the same value as
  `aicsu-section--blue`. A page does not end on a blue section.
- The theme page-title band is `main .page-header`, one per page. It prints the
  page title as an **`<h1>`**, so an interior page's content starts at `h2`.
  Only the homepage hides the band (`.home main .page-header`) and so is the
  only page whose content carries an `h1`.
- **The band is painted Pueblo Blue.** An interior page's first section cannot
  be `aicsu-section--blue`; it would merge with the band the way a trailing blue
  section merges with the footer.
- **Font Awesome 6 is loaded by the theme.** Icons are `<i class="fa-solid
  fa-*">` inside a core HTML block, no plugin and no uploads. Theme icon rules
  repaint the glyph black, so `.aicsu-card__icon` forces `currentColor`.
- **The theme leaves plain `ul`/`ol` at full section width**, so list lines run
  far past the 68ch paragraph measure. The design system sets list measure.

## Palette

Source: CSU System Brand Guidelines, 04/2020. The Fort Collins "Find Your Energy"
palette does not apply here. There is no CSU System equivalent of colostate.edu's
brand site, so this file is the reference.

| Role | Name | Hex |
|---|---|---|
| Primary | Pueblo Blue | `#1F2759` |
| Primary | CSU Gold | `#C7C271` |
| Primary | Global Red | `#AA1E40` |
| Secondary | Rose | `#C7A2A5` |
| Secondary | Pewter | `#99AFB6` |
| Secondary | Light Gold | `#CDC79B` |
| Secondary | Blush | `#E5DCDE` |
| Secondary | Sky | `#CAD8DC` |
| Secondary | Sand | `#DDDBC7` |
| Tertiary | Poppy | `#F15647` |
| Tertiary | Ocean | `#37A0A5` |
| Tertiary | Slate | `#59595B` |

Brand color hierarchy is **Pueblo Blue 60%, CSU Gold 20%, Global Red 20%**. Hold
that ratio across the site. Secondary tints support the primaries and do not
replace them. Tertiary colors are accents only, used sparingly.

The System brand guide publishes no accessibility chart. Every pairing below was
measured against WCAG 2.1; ratios are in the table and repeated inline in the CSS.
Measure any new pairing before using it.

| Background | Approved text | Ratio |
|---|---|---|
| White | Black | 21.00 AAA |
| White | Pueblo Blue | 14.07 AAA |
| White | Global Red | 7.07 AAA |
| White | Slate | 6.99 AA |
| Pueblo Blue | White | 14.07 AAA |
| Pueblo Blue | CSU Gold | 7.63 AAA |
| Sand | Pueblo Blue | 10.07 AAA |
| Sky | Pueblo Blue | 9.62 AAA |
| Blush | Pueblo Blue | 10.47 AAA |
| CSU Gold | Black | 11.38 AAA |
| Poppy | Black | 6.16 AA |
| Ocean | Black | 6.73 AA |

Never do these:

- **CSU Gold text on white** is 1.84. Gold is a background or a color on Pueblo
  Blue, never body text on white.
- **Poppy or Ocean as text on white** is 3.41 and 3.12. Both are keylines,
  icons and graphics only.
- **Global Red on Pueblo Blue** is 1.99. The two primaries never sit on each other.
- **Rose, Pewter, Light Gold, Blush, Sky, Sand as text** on white. All below 2.3.

Typography is owned by the theme. Do not set `font-family` anywhere. For reference,
the brand fonts are Industry (headlines), Proxima Nova (body sans), Minion Pro
(body serif). The guide caps a single design at three weights and four type sizes.

## Component classes

| Class | Applies to | Purpose |
|---|---|---|
| `aicsu-section` | Group block, full width | Vertical rhythm. Replaces `<hr>` dividers. |
| `aicsu-section--blue` / `--sand` / `--sky` / `--blush` | same Group | Background tint. Color only, never spacing. |
| `aicsu-section--tight` | same Group | Half vertical padding for utility strips. |
| `aicsu-inner` | nested Group | Content max-width, centered. Every section needs one. |
| `aicsu-eyebrow` | Paragraph | Small uppercase label above a heading. |
| `aicsu-lede` | Paragraph | Intro paragraph, larger than body. |
| `aicsu-cards` | Columns block | Equal-height card row. |
| `aicsu-card` | Column block | Card face with accent keyline. |
| `aicsu-card--tools/teaching/research/training/support/news/governance` | Column block | Sets the accent color. |
| `aicsu-card--plain` | Column block | Card with no accent keyline. For a grid that groups facts instead of leading somewhere. |
| `aicsu-card__icon` | HTML block, first child of a card | Tinted tile holding one Font Awesome glyph. Takes the card's accent. |
| `aicsu-card__cta` | Buttons block inside a card | Pins the button to the card's bottom edge. |
| `aicsu-btn--primary` / `--secondary` | Button block wrapper | Brand buttons. Inverts automatically on blue sections. |
| `aicsu-callout` | Group block | Bordered aside. `--action` and `--caution` variants. |
| `aicsu-table` | Table block | Comparison matrix styling. |
| `aicsu-steps` | ordered List block | Numbered process. Use only where order matters. |
| `aicsu-linklist` | List block | Resource index. |

Section pattern is always: full-width Group with `aicsu-section` → nested Group with
`aicsu-inner` → content.

## Accent keylines

The card top border is wayfinding, not decoration. One accent per card, matched to
the destination section, used nowhere else on the page:

Tools = Pueblo Blue · Teaching = Ocean · Research = Slate · Training = Poppy ·
IT Support = Slate · News = Global Red · Governance = Pueblo Blue

Five accents, not seven. CSU Gold (1.84 on white) and Pewter (2.29) are too faint
to read as a signal. Tools/Governance and Research/Support share an accent, so
cards from a shared pair must never appear in the same row.

## Icons

Font Awesome 6 ships with the theme, so icons need no plugin and no media
uploads. The tile is a core HTML block, always the card's first child:

```html
<div class="aicsu-card__icon" role="img" aria-label="Policies and governance">
  <i class="fa-solid fa-shield-halved" aria-hidden="true"></i>
</div>
```

- The tile derives its fill and border from the card's accent with `color-mix`,
  so an icon never introduces a color the card does not already carry.
- `role="img"` plus `aria-label` on the tile, `aria-hidden` on the glyph. The
  label names the subject, not the shape.
- One icon per card, `fa-solid` only. Icons are a scanning aid on card grids;
  they do not appear in body copy, headings or buttons.
- Glyphs in use: `fa-shield-halved` governance, `fa-chalkboard-user` guidelines,
  `fa-database` data, `fa-screwdriver-wrench` tools, `fa-book-open` resources,
  `fa-calendar-days` news, `fa-landmark` Board of Governors, `fa-server` CIOs,
  `fa-sitemap` campus leads. Reuse these before adding a new one.

## Working rules

- Fix problems in the CSS layer or in a synced pattern, never on an individual page.
  If a card looks wrong on one page, it is wrong everywhere.
- Local is a dev site with no public access, so edit and publish there freely.
  On production, create pages as **draft**. Never publish directly.
- Compare styling variants by pointing different CSS at the same page markup.
  Do not rebuild the page to compare looks.
- **The design system `<link>` is emitted late in the document, not in `<head>`.**
  To preview an unpushed CSS change in the browser, inject the `<style>` into
  `document.body`, not `document.head`; a head injection loses the cascade to
  the live file on equal specificity and the preview silently shows old styles.
- Prefer CSS and inline SVG over images. Images have to be re-uploaded on production.
- Screenshot the rendered page and review it there. Do not judge layout from markup.
- A draft preview (`?page_id=N&preview=true`) does not carry the `.home` body
  class, so homepage-scoped rules cannot be verified there. Check those on the
  real homepage after the content lands.

## Feedback vocabulary

When a page looks wrong, the cause is almost always one of these. Name it directly:
density, type contrast, accent count, section rhythm, image discipline, alignment.

## Writing rules

- No em dashes. Use a period, semicolon, comma, or restructure.
- No filler: leverage, circle back, excited to share, thrilled, robust, seamless.
- Direct and assertive. No hedging.
- Sentence case in body copy, Title Case for headings and buttons.
- Name things by what people do, not by how the system works.
- First reference in a piece is "Colorado State University System". Second and
  after is "CSU System". Never "CSU" alone, which means Fort Collins.
- "the" before CSU System is allowed but is not part of the name, so it stays
  lowercase.

## Migration to production

AI Engine and Tools > Import are both available on production, so either path works.

1. **Custom CSS** — one-time: add
   `<link rel="stylesheet" href="https://csu-ai.github.io/ai-wp-csusystem/aicsu-design-system.css">`
   to the theme (or a header snippet plugin) on production. Local is already
   pointed at that same URL. After that, pushes to `docs/aicsu-design-system.css`
   go live on both local and production automatically. No more manual re-paste.
2. **Pages** — either re-run the same MCP `create_post` calls against production, or
   export from local and use Tools > Import. Prefer MCP for single pages, WXR export
   for batches.
3. **Synced patterns** — these are the `wp_block` post type and travel in a WXR
   export. Verify each one after import.
4. **Media** — upload on production separately and fix URLs. Keep the media
   footprint small for this reason.
5. **Links** — local URLs need a search and replace before or after import.

Repo is public (GitHub Pages requires it). Don't commit credentials, internal
URLs, or personal-vault paths into this file or elsewhere in the repo.

Never point a write-enabled MCP connection at production without an explicit
instruction in that session.
