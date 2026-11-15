# Naftali Segal's Portfolio Design System

This document describes the design system for my portfolio website: the colours, typography, components and layout that every page is built from. It includes screenshots of the HTML/CSS mock-ups so the design is clear before the rest of the site is built.

**Design direction:** The site is aimed at recruiters in both business and technology roles, so the base is a clean, light, professional layout in navy, with a teal accent, tech tag pills and a dark footer.

---

## 1. Colour Palette

All colours are defined once as CSS custom properties (design tokens) in `:root` and used everywhere through `var()`.

| Token | Hex | Role |
| --- | --- | --- |
| `--color-primary` | `#1a4d8f` | Navy. Name, headings, links and the primary button. Carried over from my resume so both share one brand. |
| `--color-accent` | `#0f766e` | Teal. Used sparingly: the eyebrow line, the active nav underline and the tech tags. |
| `--color-accent-light` | `#f0fdfa` | Pale teal. Tag background. |
| `--color-accent-border` | `#99f6e4` | Light teal. Tag border. |
| `--color-text` | `#1f2937` | Body text. Near-black, which is easier to read than pure black. |
| `--color-muted` | `#4b5563` | Secondary text: taglines and card descriptions. |
| `--color-header-bg` | `#cbd5e1` | Light slate. Header background. |
| `--color-bg` | `#f8fafc` | Page background (very light grey). |
| `--color-surface` | `#ffffff` | Cards and the hero section. |
| `--color-border` | `#e5e7eb` | Card borders and dividers. |
| `--color-footer` | `#0f172a` | Dark navy footer background. |
| `--color-footer-text` | `#cbd5e1` | Footer text and links. |

---

## 2. Typography

- **Font:** Inter, with Arial as a fallback. Inter is clean, modern and easy to read on screens.
- **One font for the whole site.** Headings stand out through size and colour instead of different fonts:
  - **Name and section headings:** large, bold, navy
  - **Card titles:** bold, dark text
  - **Eyebrow line and tags:** small, teal
  - **Taglines and descriptions:** grey (muted)
  - **Body text:** regular, dark text

---

## 3. Components

### Header and Navigation

- **Design:** Light slate background, with my name on the left and the navigation links on the right. The current page and hovered links turn navy with a teal underline.
- **Why the tinted header:** a white header right above the white hero section had no visual break. The slate tint separates the navigation from the content.
- **Phones:** the name and links stack and are centred.

![Header Mock-up](design/header.png)

### Hero

- **Design:** A spacious white section with a small teal line (program and school), my name as the biggest heading, a one-sentence tagline in grey, and two buttons.

![Hero Mock-up](design/hero.png)

### Buttons

- **Design:** Rounded buttons with a navy border, in two styles:
  - **Primary:** filled navy with white text, for the main action.
  - **Secondary:** outlined in navy, for the secondary action.
- Only one primary button per section, so the main action stands out.

![Buttons Mock-up](design/buttons.png)

### Project Card (reusable component)

- **Design:** White card with a light border and rounded corners. Each card has:
  1. **Image (optional):** a screenshot or logo, always cropped to the same rectangular shape so every card matches.
  2. **Title**
  3. **Short description** in grey
  4. **Tech tags:** small teal labels for the technologies used.
- Every project uses this same card, so new projects (Yatzy, Hospital Triage) can be added without new styles.

![Project Card Mock-up](design/card.png)

### Footer

- **Design:** Dark navy background with light text. Copyright on the left, GitHub / LinkedIn / Email links on the right. The dark footer gives every page a clear ending.
- **Phones:** stacks and is centred.

![Footer Mock-up](design/footer.png)

---

## 4. Layout

- **Content width:** content stays in a centred column so it doesn't stretch too wide on big monitors, while the header, hero and footer backgrounds still go edge to edge.
- **Project grid:** cards sit side by side on a laptop and stack one per row on a phone.
- **Spacing:** sections have plenty of space between them. On phones, all sections line up along the same left edge.
- **Phones:** the header and footer stack, spacing shrinks, and the name gets smaller.

### Full page (desktop)

![Full Page Mock-up](design/full-page.png)

### Mobile

![Mobile Mock-up](design/mobile.png)

---

## 5. Design Tokens in Code

```css
:root {
    --color-primary: #1a4d8f;
    --color-accent: #0f766e;
    --color-text: #1f2937;
    --color-muted: #4b5563;
    --color-border: #e5e7eb;
    --color-bg: #f8fafc;
    --color-surface: #ffffff;
    --color-footer: #0f172a;
    --color-footer-text: #cbd5e1;
    --color-accent-light: #f0fdfa;
    --color-accent-border: #99f6e4;
    --color-header-bg: #cbd5e1;

    --font-main: "Inter", Arial, sans-serif;
    --radius: 8px;
}
```

## 6. Changes in PD2

PD2 adds a technical write-up of my Yatzy game (`yatzy.html`). The page is built from the existing design system: page intro, cards, tech tags, buttons, figures, the resume's skills list, header and footer. **No colours, fonts or design tokens were added or changed.** Every new style uses the existing tokens from section 5.

The new pieces below were added because the Yatzy write-up needed things PD1 didn't have (a table, code samples), or because building the page showed a problem in the PD1 CSS.

### New components

#### Data table

- **Used for:** the Yatzy API endpoint table.
- **Design:** white surface with a light border, a pale teal header row (`--color-accent-light`) with navy headings (`--color-primary`), and a thin line between rows. The caption sits above in grey (`--color-muted`).
- **Phones:** the table sits in a `.table-wrap` wrapper that scrolls sideways, so a wide table never pushes the page wider than the screen.
- **Classes:** `.table-wrap`, `.data-table`

![Data table](design/data-table.png)

#### Code

- **Inline code** (any `<code>` element in a sentence): monospace font with a light grey tint (`--color-bg`), so names like `fetch` stand out from the text.
- **Code block** (`.code-block`): a dark panel for JSON samples. It reuses the footer's colours (`--color-footer` background, `--color-footer-text` text), so it needs no new colour. Long lines scroll instead of breaking the layout.

![Code block](design/code-block.png)

#### Skip link

- **Used for:** keyboard and screen reader users. It is the first link on every page and jumps past the navigation to the main content (`<main id="main">`).
- **Design:** hidden off screen until it receives keyboard focus, then appears in the top-left corner as a navy button over the header. Mouse users never see it.
- **Why off screen and not `display: none`:** `display: none` would also remove it from the Tab order, so keyboard users couldn't reach it.
- **Class:** `.skip-link`

![Skip link shown after pressing Tab](design/skip-link.png)

### New modifiers

Modifiers change one existing component instead of creating a new one.

| Modifier | Added to | What it does |
| --- | --- | --- |
| `.figure-narrow` | `.project-figure` | Caps the figure at 320px, so a tall phone screenshot doesn't fill the whole screen |
| `.card-grid-pairs` | `.card-grid` | Always two columns (one on phones). Four cards in the normal three-column grid left one card alone on the last row |

![Two-column card grid](design/card-grid-pairs.png)

### Changed

- **Button spacing.** PD1 spaced buttons with `.btn + .btn { margin-left: 0.5rem; }`. On phones the buttons wrap onto two lines, and that rule only adds space to the side, so the stacked buttons touched. It is replaced by a `.hero-buttons` group (`display: flex; flex-wrap: wrap; gap: 0.5rem;`), which spaces buttons both side by side and when stacked. The home page hero already used the `hero-buttons` class but it had no styles, so this also fixes the home page.

![Buttons stacked on a phone, with space between them](design/buttons-mobile.png)

- **Section spacing.** PD2 pages stack grids, cards and figures in one section, so each now gets a 1.5rem gap below it instead of touching. When two sections follow each other, the second drops its top padding, so the gap between them is 3rem instead of 6rem.
- **Navigation.** The Yatzy page has no nav item of its own. "Projects" is marked active on it, because Yatzy is one of my projects, and it is linked from the Home and Projects pages.

---

## Conclusion

This design system is the blueprint for the portfolio. It defines one palette, one type scale and a small set of reusable components, so every page stays consistent as new projects are added throughout the semester.
