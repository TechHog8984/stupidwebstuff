# techhog / iCceph theme — style guide

Use this to build new single-page HTML tools that visually match `icceph-deobfuscator.html`.
It's a **dark amber terminal / dev-tool** aesthetic — think a reverse-engineering utility, not a marketing site.

## Attribution (keep on every page)

- Small eyebrow line above the title: `made by techhog`
- If the page is Claude/AI-generated, a subtitle under the title crediting that, in the same self-aware, slightly dry tone as:
  > This site was completely vibe coded by Sonnet 5 (except for the [core logic] code)

## Color tokens

```css
--bg: #10131a;          /* page background */
--panel: #171b24;       /* textarea / card background */
--panel-border: #2a2f3d;/* default borders */
--amber: #e8a33d;       /* primary accent — buttons, active states, title highlights */
--amber-dim: #8a6a2f;   /* secondary accent — eyebrow text, idle dots, focus borders */
--text: #cfd4e0;        /* body text */
--text-dim: #6b7182;    /* secondary/muted text */
--mono: 'IBM Plex Mono', 'Courier New', monospace; /* the one font stack, reused everywhere */
```

Optional secondary accent for "success"/output-style text: soft green `#a8e6b0` (used sparingly, e.g. output panel text only — don't let it compete with amber as the primary accent).

Always declare the font stack once as `--mono` and reference it with `font-family: var(--mono)` — don't retype the raw font stack per page. This is what keeps every page rendering identically instead of silently drifting to a fallback font.

## Typography

- Font: **IBM Plex Mono** for everything (headings, body, UI, buttons) — loaded via Google Fonts:
  ```html
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600;700&display=swap" rel="stylesheet">
  ```
- No serif, no secondary display face — monospace is the whole personality of this theme.
- `html, body` set `font-family: var(--mono)` and nothing else font-related (no default `font-size`/`line-height` on body). Every text element declares its own `font-size` explicitly — this is deliberate, don't rely on inheritance, or pages will drift out of sync with each other.
- Title (`h1`): exactly 30px, weight 700, near-white (`#f2f4f8`), letter-spacing `-0.01em`, `margin: 0 0 12px`.
- Eyebrow (`made by techhog` line): exactly 12px, uppercase, letter-spacing `0.18em`, color `--amber-dim`, `margin: 0 0 10px`.
- Field / section labels (the small caption above an input, output, or list): exactly 11px, uppercase, letter-spacing `0.14em`, color `--text-dim`, `margin-bottom: 8px`.
- Subtitle: exactly 13.5px, italic, `--text-dim`, `margin: 0`.
- Body/UI text (buttons, textareas, list items): 13px, line-height ~1.55, set explicitly on that element.

## Layout

- Single centered column, `max-width: 920px`, generous top padding (~56px).
- Faint grid background on `<body>` using repeating amber-tinted 1px lines at low opacity (~0.03–0.04), 28px cell size:
  ```css
  background-image:
    linear-gradient(rgba(232,163,61,0.035) 1px, transparent 1px),
    linear-gradient(90deg, rgba(232,163,61,0.035) 1px, transparent 1px);
  background-size: 28px 28px;
  ```
- Header block: `margin-bottom: 40px`, `padding-bottom: 24px`, separated from content by a `1px solid var(--panel-border)` bottom rule. Use these exact numbers on every page — don't re-derive them.
- Panels (textareas, cards, etc.) use `--panel` background, `--panel-border` border, `4px` border-radius — sharp/utilitarian, not soft/rounded.
- Field labels get a small square "status dot" before them (6x6px, `border-radius: 1px`) — dim by default, lights up to `--amber` when that field has been used/is active. This is the page's signature micro-detail; reuse it for any labeled input/output pair.

## Components

**Buttons (primary action)**
```css
background: transparent;
border: 1px solid var(--amber);
color: var(--amber);
border-radius: 4px;
font-weight: 600;
letter-spacing: 0.06em;
```
On hover: fill with `--amber`, text flips to `--bg`, add a soft amber glow (`box-shadow: 0 0 24px rgba(232,163,61,0.25)`). On active: `translateY(1px)`.

Prefix primary action labels with a shell-style caret, e.g. `>_ run`, `>_ deobfuscate`, `>_ encode` — reinforces the terminal/command feel.

**Text areas / inputs**
- Monospace, 13px, `--panel` background, `--panel-border` border, 16px padding, resizable vertically.
- Focus state: border brightens to `--amber-dim` (not full `--amber` — keep focus subtle).
- Placeholder text: very dim, `#454b5c`.
- If a field is a "result"/output field, it's fine to tint its text a soft green (`#a8e6b0`) to differentiate it from input, and mark it `readonly`.

## Tone / voice

- Dry, self-aware, slightly deadpan — the copy can acknowledge it's AI-built without being cutesy about it.
- No marketing language, no exclamation points, no emoji.
- UI copy is plain and literal: label things by what they are (`Input`, `Output`) not clever names.
- Footer/meta text (if any) should read like a terminal status line, not a tagline.

## What to avoid

- No rounded/soft "SaaS landing page" look (large border-radius, drop shadows, gradients as decoration).
- No serif or display fonts — breaks the terminal identity.
- No color outside the amber/dark palette except the muted green for output/success text.
- No unnecessary animation — the theme's only "motion" should be simple hover/focus transitions (~0.15s ease). Avoid blinking cursors, particle effects, scroll reveals, etc.
- Don't reuse the exact copy from other tools in this theme (e.g. don't reuse "deobfuscate" wording for an unrelated tool) — adapt field labels and button verbs to whatever the new tool actually does, while keeping the visual system identical.
- No javascript unless explicitly asked.

## Quick checklist for a new page in this theme

- [ ] `made by techhog` eyebrow above the title
- [ ] IBM Plex Mono loaded, used everywhere
- [ ] Dark bg + faint amber grid overlay
- [ ] Amber primary accent, dim-amber secondary, panel/border greys as specified
- [ ] Sharp 4px-radius panels, no heavy shadows
- [ ] Status-dot field labels (dim → amber when active)
- [ ] `>_`-prefixed primary button, amber outline → amber fill on hover with glow
- [ ] Dry, plain, non-marketing copy
