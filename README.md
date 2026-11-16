# SpendWise Dashboard Shell

A static, responsive budget dashboard layout built with HTML and CSS only. It shows realistic sample data and has no JavaScript or working features yet. It is the visual foundation for the SpendWise capstone project.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Page structure: sidebar, header, and six category cards |
| `style.css` | All styling: theme variables, layout, components, responsive rules, dark theme |
| `Spendwise_Logo.png` | Logo shown in the sidebar (must be in the same folder) |

To view it, open `index.html` in a browser. The Google Fonts (Inter and Poppins) need an internet connection and fall back to system fonts if offline.

## Page structure

```
.app (CSS Grid)
├── aside.sidebar      logo + navigation
├── header.topbar      page title + monthly total + avatar
└── main.content       heading + .cards grid
    └── article.card   x6 (Food, Transport, Rent, Entertainment, Savings, Utilities)
```

### Sidebar
Holds the logo on a white tile (so it stays readable on the navy background) and a navigation list with six links: Dashboard (marked active with `aria-current="page"`), Expenses, Categories, Reports, Savings Goals and Settings. The links are placeholders (`href="#"`).

### Header
Shows the page title, the month, the total spent against the total budget ($2,380 of $2,870), and an avatar with initials.

### Category cards
Each card shows an icon, the category name and description, the amount spent against its budget, a progress bar, and a footer with percent used and the amount left. Rent and Utilities use the gold warning bar because they are at or near their budget. The progress bar width comes from a `--pct` custom property set inline on each card, for example `style="--pct:70%"`.

## How the CSS is organized

1. **Theme:** colors, shadows and radius live as CSS custom properties on `:root`.
2. **Base:** box-sizing, fonts, and heading styles.
3. **Page layout:** `.app` uses CSS Grid with named areas (`sidebar`, `header`, `main`) and a 250px sidebar column.
4. **Sidebar:** Flexbox column for the logo and nav; each nav link is a Flexbox row of icon and label.
5. **Header:** Flexbox row with `space-between`, wrapping on narrow widths.
6. **Cards:** `.cards` is a Grid (`repeat(auto-fill, minmax(260px, 1fr))`), and each `.card` is a Flexbox column. The card top row and footer are Flexbox rows.
7. **Responsive:** the media query for narrow screens.
8. **Reduced motion:** disables the card animation for users who ask for less motion.

No absolute positioning is used for the layout. The sidebar uses `position: sticky` on desktop so it stays in view while the page scrolls.

## Theme variables

| Variable | Role |
| --- | --- |
| `--brand` | Navy from the logo: sidebar and headings |
| `--accent` | Green from the logo: progress bars, active nav item, avatar |
| `--warn` | Gold from the logo: bars for budgets that are full or nearly full |
| `--surface` | Card and header background |
| `--bg` | Page background |
| `--text` | Primary text |
| `--text-muted` | Secondary text |
| `--border`, `--track`, `--accent-soft`, `--brand-text` | Supporting colors |
| `--shadow`, `--shadow-lift`, `--radius` | Card shadow, hover shadow, corner radius |

Every color in the stylesheet comes from these variables, so changing the theme means editing only the `:root` block.

## Responsive behavior

Below 768px (`max-width: 767px`):

- The grid becomes one column, with the sidebar first, then the header, then the cards.
- The sidebar stops being sticky, the logo shrinks, and the nav becomes a horizontally scrolling row.
- The cards stack in a single column.

To check it, open DevTools, switch on the Device Toolbar (Ctrl+Shift+M), and choose a phone size or drag the width below 768px.

## Card micro-interactions

On hover and on keyboard focus, a card lifts 4px (`transform: translateY(-4px)`) and gets a deeper shadow (`box-shadow`). The transition lasts 200ms and animates only `transform` and `box-shadow`. Cards have `tabindex="0"` so they can be reached with the Tab key, and a visible green outline marks keyboard focus. Users with the "reduce motion" setting see no movement.

## Dark theme (stretch goal)

An `@media (prefers-color-scheme: dark)` block overrides only the `:root` variables, so no other rule changes. To test it, open DevTools, then Rendering, then Emulate CSS media feature `prefers-color-scheme`, and choose `dark`.

## Accessibility notes

- Semantic elements are used: `aside`, `nav`, `header`, `main`, `article`.
- Decorative emoji icons are hidden from screen readers with `aria-hidden="true"`.
- Progress bars use `role="progressbar"` with `aria-valuenow`, `aria-valuemin`, `aria-valuemax` and a label.
- Keyboard focus is visible on both nav links and cards.
