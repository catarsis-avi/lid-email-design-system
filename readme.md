# La Izquierda Diario Chile — Email Design System

Design system for LID's transactional/editorial **email HTML** — real code meant to be pasted into a mailing tool (Mailchimp, Brevo, etc.), not images exported from Canva. Canva stays useful for loose visual assets (photos, carousel-style covers); structure, copy and layout live in HTML here.

**Sources given:** clean logo exports in `assets/` — icon mark in navy/burgundy/tan (`logo-mark-*.png`) and full wordmark (icon + "LA IZQUIERDA DIARIO") in navy/burgundy/cream (`logo-wordmark-*.png`), all transparent PNGs, auto-cropped to their bounding box. No codebase, Figma file, or brand guideline PDF was attached; the palette/type/component spec below comes from the brief pasted by the user, itself derived from LID's Instagram carousel system.

## A note on how this is authored

This project's compiler expects reusable templates as Design Components (`templates/<slug>/*.dc.html`, React-rendered). **Email HTML cannot be authored that way** — an ESP needs literal `<table>`/inline-`style` markup with Outlook conditional comments, `<!--[if mso]-->`, `color-scheme` meta tags, etc.; a DC's rendering pipeline doesn't produce that raw, paste-ready source. So the actual deliverable — the 8 components and 3 full examples — are plain, self-contained `.html` files under `email/`, each tagged `@dsCard` so they still show in the Design System tab. Every component file marks its copy-paste region with `COPY FROM HERE / TO HERE` comments.

## Index

- `styles.css` + `tokens/` — CSS custom properties for colors, type, spacing (documentation/preview only; production email uses inline styles, per email-client requirements).
- `assets/` — logo files.
- `guidelines/` — foundation specimen cards (colors, type, spacing, buttons, brand marks) + `assembly-guide.html`.
- `email/components/` — the 8 reusable snippets: header, hero, note module, CTA button, divider, quote block, legal/transparency block, footer.
- `email/examples/` — 3 full assembled emails: `newsletter.html`, `campaign.html`, `lifecycle.html`.
- `thumbnail.html` — project tile.

## Content fundamentals

- Spanish (Chile), direct and organizing-oriented — copy addresses the reader as compañero/a implicitly via plural/collective framing, not corporate "usted" nor over-familiar "tú" marketing voice.
- No sustained uppercase in body copy — caps only for brand name treatment ("LA IZQUIERDA DIARIO") and short eyebrow labels (category pills, "PASO 1").
- No emoji — matches the outlet's serious editorial tone.
- Headlines are factual/news-style ("Profesores votan continuidad del paro en asamblea nacional"), not clickbait. Deks are one sentence of context, not a teaser.
- CTAs are concrete verbs tied to political action: "Firmar la petición", "Leer la nota completa", "Suscríbete" — not generic "Click here"/"Learn more".
- Never shrink line-height or font size to force text to fit — cut the copy instead.

## Visual foundations

- **Two primary dynamics** (from the Instagram carousel template, the ground truth for color pairing): (1) **burgundy background** `#9f334e` with cream text `#fdf4e3` and the cream/tan logo mark; (2) **cream background** `#fdf4e3` with navy text `#003874` and the **burgundy** logo mark. These two covers the large majority of screens/emails. Navy as a *background* is an occasional accent only (e.g. one hero in a newsletter for variety), not a third equal-weight dynamic.
- **Logo/background pairing rule — strict**: cream background → burgundy logo, always. Never the navy logo on cream. The navy logo is reserved for very particular special cases (e.g. reversed on a navy background) — default to burgundy or cream logo lockups everywhere else.
- **Colors**: cream `#fdf4e3` (dominant reading surface, dynamic 2), navy `#003874` (text-on-cream + rare accent background) and burgundy `#9f334e` (dynamic 1 background, dynamic 2 logo). Max 3 colors per screen. A neutral legal tint `#f2e6cd` (cream, darkened) exists only for the transparency/legal block. No gradients, no shadows, never mix text colors within one block.
- **Eyebrow/label accent**: a short vertical bar precedes the category label (cream bar on burgundy bg, burgundy bar on cream bg) — same accent-bar language as the carousel template.
- **Type**: DM Sans (700/800 display, 400 body) as the primary family; Barlow Condensed 700 uppercase/tracked for eyebrows, category pills, and dates. Both fail in Outlook desktop — Arial/Helvetica fallback is designed to look intentional on its own, not like a broken DM Sans.
- **Spacing**: 8/12/20/32/48px scale. Fixed 600px email canvas, fluid to 100% width, 24px side gutter.
- **Backgrounds**: flat color fields only (cream, navy, burgundy) — no photos as backgrounds, no full-bleed imagery, no texture/pattern/grain. Photography appears only inside note modules as a discrete rectangular image, never with text overlaid without a solid block behind it.
- **Buttons**: single treatment per color — solid fill, cream text, 4px corner radius, generous padding, no shadow, no border. Built as a table cell + anchor, never `<button>`.
- **Cards/modules**: no border, no shadow, no rounded corners on note modules — separation comes from whitespace and a 1px navy hairline divider, not containers.
- **Motion/hover/press states**: none — email clients don't support hover/press or animation reliably; no interaction states are designed.
- **Corner radii**: 14px soft-rounded on buttons, note-module images, and the legal/transparency block; the category pill keeps full pill radius (999px). Sharp rectangles are avoided everywhere.
- **Transparency/blur**: not used — unsupported across email clients.

## Iconography

No icon system, icon font, or SVG icon set was found in the provided assets — the corner-overlay reference shows a plain outline globe glyph flattened into a composite image, not an extractable icon file. Per the "never hand-roll SVG/icon" rule, the footer uses **plain text links** ("laizquierdadiario.cl · Instagram · X · TikTok") instead of icon glyphs — also more robust across email clients that block images by default. If LID has real social-icon PNGs/SVGs, drop them in `assets/icons/` and swap the footer's text links for `<img>` tags (keep `alt` text).

## Fonts — substitution flag

No font files were provided. `tokens/typography.css` declares `@font-face` for DM Sans / Barlow Condensed pointing at Google's hosted webfont files (some URLs are the commonly-referenced ones for these families and should be spot-checked against Google Fonts' current CSS2 API before going live — reliable in all cases: `<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;700;800&family=Barlow+Condensed:wght@700&display=swap">`, used in every specimen/example here). **Ask LID if they have licensed font files** to self-host instead — otherwise this Google Fonts link is what production emails should use, understanding Outlook desktop will always fall back to Arial/Helvetica regardless.

## Design tokens

See `tokens/colors.css`, `tokens/typography.css`, `tokens/spacing.css` (imported by `styles.css`). These exist for internal documentation/preview consistency — actual email HTML must inline every value (see Technical rules below), CSS variables are not supported by Outlook/Gmail.

## Mandatory technical rules (see `email/components/` for the implementation)

Table layout only (`role="presentation"`), CSS inlined on every element with a `<style>` block in `<head>` as reinforcement only, fixed 600px width fluid to 100%, Outlook conditional comments for width/font fixes, `color-scheme`/`supported-color-schemes` meta tags with explicit background/text color on every cell (never inherited), buttons as table cells (never `<button>`), every image has `width`, `height`, `alt` — headline and CTA copy always live as real HTML text, never image-only, hidden per-send preheader as the first element in `<body>`.
