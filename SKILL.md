---
name: la-izquierda-diario-email-design
description: Use this skill to generate on-brand HTML emails for La Izquierda Diario Chile (LID) — newsletters, one-off campaigns, and lifecycle automations — ready to paste into a mailing tool (Mailchimp, Brevo, etc.), either for production or drafts/mocks.
user-invocable: true
---

Read `readme.md` in this skill for brand context, content fundamentals, visual foundations, and design tokens. Explore `tokens/` for colors/type/spacing, `assets/` for logos, `guidelines/` for foundation specimens, `email/components/` for the 8 reusable HTML snippets (header, hero, note module, CTA button, divider, quote block, legal/transparency block, footer — each copy-paste ready, marked with COPY FROM HERE / TO HERE comments), and `email/examples/` for 3 fully assembled emails (newsletter, one-off campaign, lifecycle).

When asked to build an email: pick the assembly pattern from `guidelines/assembly-guide.html` matching the email type, compose it from the component snippets (don't reinvent the table/inline-style structure), keep the mandatory technical rules in `readme.md` (table layout, inline CSS, Outlook conditional comments, color-scheme meta tags, explicit background/text color per cell, table-cell buttons, image width/height/alt, unique per-send preheader). Never reduce line-height or font size to fit text — shorten the copy instead. Max 3 colors per screen (cream/navy/burgundy). No emoji, no sustained uppercase body copy, no icon glyphs (LID has no icon system — use plain text links).

If the user just invokes this skill with no brief, ask what kind of email they need (newsletter, campaign, lifecycle step) and what content/CTA it should carry, then assemble it from the components above.
