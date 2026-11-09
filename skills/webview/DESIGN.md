# Design

The look is **quiet**: a neutral palette, one accent colour, generous whitespace, and hierarchy carried by type size and weight rather than colour or borders. It should feel like well-made product documentation, branded to no one: no tool or vendor branding anywhere on the page.

## Self-contained file

- One `.html` file with all CSS and JS inline. No CDNs, no web fonts, no external requests. It must work offline when emailed or dropped into a chat.
- Fonts: system stacks only. Sans: `system-ui, -apple-system, "Segoe UI", Roboto, sans-serif`. Mono: `ui-monospace, SFMono-Regular, Menlo, Consolas, monospace`.
- Images: embed as base64 `data:` URIs. Downscale anything wider than ~1600px first, if a tool for that is available. If the total would exceed ~15 MB, save the page as `~/webview/<slug>/index.html` with an `assets/` folder beside it instead.
- Diagrams: hand-written inline SVG that uses the colour tokens, so it adapts to both themes. Keep labels as real `<text>`, and give each diagram a one-line caption.
- Vanilla JS only, and only what's needed (navigation, theme toggle, search, slides, copy buttons). The page must remain readable with JS off.

## Tokens and theme

- Define every colour as a CSS variable on `:root`: background, surface, text (~85% contrast), muted text (~60%), hairline, one accent, plus success/warning/danger for badges and callouts.
- Dark mode: redefine the tokens under `@media (prefers-color-scheme: dark)`. Add a small light/dark toggle that sets `data-theme` on `<html>`, so the toggle wins over the system setting.
- Type: base 16px, line-height 1.6. Headings: h1 32px, h2 22px, h3 17px, weight 600. Wrap body text at a measure of ~70ch.

## Components

- **Hero**: title, one-line subtitle, date generated.
- **Tiles**: key facts, metrics or decisions in a responsive grid.
- **Tables**: hairline row dividers and a sticky header. On narrow screens, wide tables scroll inside their own container.
- **Callouts**: info, warning, decision and open question, each with a left accent bar.
- **Badges**: status and priority.
- **Expandable sections**: `<details>` / `<summary>` for depth.
- **Code blocks**: monospace with a copy button.
- **Timeline / steps**: numbered markers on a vertical line.

## Formats

- **Document**: sticky left sidebar with section links and scroll-spy highlighting, and a content column of ~760px max width. Below 800px the sidebar collapses into a top menu. Every heading gets an anchor link. For the Look up goal, add a client-side search box that filters sections.
- **Slides**: full-viewport sections, one idea per slide, with a large heading and at most ~6 short lines or one visual. Navigate with arrow keys, space and on-screen buttons. Show a slide counter and update the URL hash per slide. Press `o` for a grid overview. Print one slide per page.
- **Dashboard**: a header with the headline status, a tile row of metrics, then a card grid (status, findings, risks, next steps). Each card expands to show detail. Use a single column on phones.

## Always

- Use a 16px side gutter on phones and allow no horizontal page scroll.
- Smooth scroll for in-page links, and no other motion. Respect `prefers-reduced-motion`.
- Include `@media print`: hide navigation and toggles, and expand every `<details>`.
- Use semantic HTML (`header`, `nav`, `main`, `section`) and meaningful `alt` text, keep colour contrast at WCAG AA or better, and show visible focus styles.
