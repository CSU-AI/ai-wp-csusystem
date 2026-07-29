# ai.colostate.edu build context

Campus AI site for CSU Fort Collins. Owner: David Edwards, AI Strategist, CSU System.
Build locally first, then migrate to production.

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

## Palette

Source: https://brand.colostate.edu/color/ (Find Your Energy brand).
Previous CSU secondary and tertiary palettes are retired.

| Role | Name | Hex |
|---|---|---|
| Primary | Colorado State Green | `#1E4D2B` |
| Primary | Colorado State Gold | `#C8C372` |
| Primary | Aggie Orange | `#D9782D` |
| Primary | 80% Black | `#59595B` |
| Energy | Oval Green | `#006144` |
| Energy | Lovers Lane | `#82C503` |
| Energy | Energy Green | `#CFFC00` |
| Energy | Flower Trial Red | `#E56A54` |
| Energy | Powered Purple | `#7E5475` |
| Energy | Horsetooth Blue | `#008FB3` |
| Energy | Stalwart Slate | `#105456` |
| Energy | Sunshine | `#FFC038` |
| Neutral | Gray | `#CCCCCC` |
| Neutral | Tan | `#E3CDB1` |

**Only use pairings on CSU's published accessibility chart.** Pairings not on the
chart are not approved for university use. The ones this site relies on:

| Background | Approved text |
|---|---|
| White | Black (AAA), Primary Green (AAA), Stalwart Slate (AAA), Oval Green (AAA), 80% Black (AA) |
| CSU Green | White (AAA), Energy Green (AAA), Gold (AA) |
| Tan | Primary Green (AA), Stalwart Slate (AA), Oval Green (AA) |
| Gray | Black (AAA), Primary Green (AA), Stalwart Slate (AA), Oval Green (AA) |
| Sunshine | Black (AAA), Primary Green (AA) |

Target proportions across the site, per brand guidance: roughly one third CSU Green,
one sixth white, then Gold, Oval Green, and Energy Green at about 9% each, with the
remaining Energy colors used sparingly.

Typography is owned by the theme. Do not set `font-family` anywhere.

## Component classes

| Class | Applies to | Purpose |
|---|---|---|
| `aicsu-section` | Group block, full width | Vertical rhythm. Replaces `<hr>` dividers. |
| `aicsu-section--green` / `--tan` / `--gray` | same Group | Background tint. Color only, never spacing. |
| `aicsu-section--tight` | same Group | Half vertical padding for utility strips. |
| `aicsu-inner` | nested Group | Content max-width, centered. Every section needs one. |
| `aicsu-eyebrow` | Paragraph | Small uppercase label above a heading. |
| `aicsu-lede` | Paragraph | Intro paragraph, larger than body. |
| `aicsu-cards` | Columns block | Equal-height card row. |
| `aicsu-card` | Column block | Card face with accent keyline. |
| `aicsu-card--tools/teaching/research/training/support/news/governance` | Column block | Sets the accent color. |
| `aicsu-card__cta` | Buttons block inside a card | Pins the button to the card's bottom edge. |
| `aicsu-btn--primary` / `--secondary` | Button block wrapper | Brand buttons. Inverts automatically on green sections. |
| `aicsu-callout` | Group block | Bordered aside. `--action` and `--caution` variants. |
| `aicsu-table` | Table block | Comparison matrix styling. |
| `aicsu-steps` | ordered List block | Numbered process. Use only where order matters. |
| `aicsu-linklist` | List block | Resource index. |

Section pattern is always: full-width Group with `aicsu-section` → nested Group with
`aicsu-inner` → content.

## Accent keylines

The card top border is wayfinding, not decoration. One accent per card, matched to
the destination section, used nowhere else on the page:

Tools = CSU Green · Teaching = Powered Purple · Research = Horsetooth Blue ·
Training = Aggie Orange · IT Support = Stalwart Slate · News = Gold ·
Governance = Oval Green

## Working rules

- Fix problems in the CSS layer or in a synced pattern, never on an individual page.
  If a card looks wrong on one page, it is wrong everywhere.
- Create pages as **draft**. Never publish directly.
- Compare styling variants by pointing different CSS at the same page markup.
  Do not rebuild the page to compare looks.
- Prefer CSS and inline SVG over images. Images have to be re-uploaded on production.
- Screenshot the rendered page and review it there. Do not judge layout from markup.

## Feedback vocabulary

When a page looks wrong, the cause is almost always one of these. Name it directly:
density, type contrast, accent count, section rhythm, image discipline, alignment.

## Writing rules

- No em dashes. Use a period, semicolon, comma, or restructure.
- No filler: leverage, circle back, excited to share, thrilled, robust, seamless.
- Direct and assertive. No hedging.
- Sentence case in body copy, Title Case for headings and buttons to match the
  rest of colostate.edu.
- Name things by what people do, not by how the system works.

## Migration to production

AI Engine and Tools > Import are both available on production, so either path works.

1. **Custom CSS** — one-time: add a `<link rel="stylesheet" href="https://<pages-url>/aicsu-design-system.css">`
   to the theme (or a header snippet plugin) on production, pointed at the GitHub
   Pages URL. After that, pushes to `docs/aicsu-design-system.css` go live on both
   local and production automatically. No more manual re-paste.
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
