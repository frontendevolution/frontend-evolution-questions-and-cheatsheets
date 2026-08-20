# CSS Grid — The Complete Reference (2026)
**Pillar:** Foundations Done Right · **Category:** HTML & CSS · **Level:** Advanced
*The one doc to keep open while coding, reviewing, or doing final interview prep.*

---

## 1. Core Definitions & Vocabulary

- **Grid container** — the element with `display: grid` or `display: inline-grid`; establishes a grid formatting context for its direct children.
- **Grid item** — a direct child of a grid container, automatically participating in grid layout.
- **Grid line** — the dividing lines that make up the grid structure, numbered from 1, both positive (start) and negative (from the end).
- **Grid track** — the space between two adjacent grid lines — a row or a column.
- **Grid cell** — the smallest unit of the grid: the intersection of one row track and one column track.
- **Grid area** — a rectangular region made of one or more cells, either named (via `grid-template-areas`) or spanned via line numbers.
- **Explicit grid** — the tracks you define directly with `grid-template-columns`/`grid-template-rows`.
- **Implicit grid** — tracks the browser auto-generates when content overflows the explicit grid, sized via `grid-auto-rows`/`grid-auto-columns`.
- **Gutter/gap** — the space between tracks, set via `gap`, `row-gap`, `column-gap`.
- **Subgrid** — a grid item that is itself a grid container and inherits its parent's tracks instead of defining its own.
- **`fr` unit** — a fraction of the leftover space in the grid container after fixed tracks and gaps are subtracted.

---

## 2. Grid Container Properties (Full Enumeration)

Every property that applies to the **grid container** (the parent):

1. **`display`** — `grid` | `inline-grid` (block-level vs inline-level grid container).
2. **`grid-template-columns`** — defines column track sizes (lengths, `%`, `fr`, `auto`, `minmax()`, `repeat()`, named lines).
3. **`grid-template-rows`** — defines row track sizes, same value types as columns.
4. **`grid-template-areas`** — defines named regions using a string-based ASCII grid; `.` denotes an empty cell.
5. **`grid-template`** — shorthand for `grid-template-rows` / `grid-template-columns` / `grid-template-areas` combined.
6. **`grid-auto-columns`** — sizes implicit columns created when content overflows the explicit grid.
7. **`grid-auto-rows`** — sizes implicit rows created when content overflows the explicit grid.
8. **`grid-auto-flow`** — controls auto-placement algorithm direction; values: `row` | `column` | `dense` | `row dense` | `column dense`.
9. **`grid`** — shorthand resetting and combining all six template + auto-flow properties above in one declaration.
10. **`gap`** (formerly `grid-gap`) — shorthand for `row-gap` + `column-gap`.
11. **`row-gap`** (formerly `grid-row-gap`) — space between row tracks.
12. **`column-gap`** (formerly `grid-column-gap`) — space between column tracks.
13. **`justify-items`** — aligns items along the inline (row) axis inside their cell; values: `start` | `end` | `center` | `stretch` (default).
14. **`align-items`** — aligns items along the block (column) axis inside their cell; values: `start` | `end` | `center` | `stretch` (default) | `baseline`.
15. **`place-items`** — shorthand for `align-items` + `justify-items`.
16. **`justify-content`** — aligns the entire grid within the container on the inline axis, when tracks don't fill it; values: `start` | `end` | `center` | `stretch` | `space-between` | `space-around` | `space-evenly`.
17. **`align-content`** — aligns the entire grid within the container on the block axis; same value set as `justify-content`.
18. **`place-content`** — shorthand for `align-content` + `justify-content`.

---

## 3. Grid Item Properties (Full Enumeration)

Every property that applies to a **grid item** (the child):

1. **`grid-column-start`** — starting column line (number, named line, or `span N`).
2. **`grid-column-end`** — ending column line.
3. **`grid-row-start`** — starting row line.
4. **`grid-row-end`** — ending row line.
5. **`grid-column`** — shorthand: `grid-column-start / grid-column-end`.
6. **`grid-row`** — shorthand: `grid-row-start / grid-row-end`.
7. **`grid-area`** — shorthand for all four line properties, OR assigns the item to a named area from `grid-template-areas`.
8. **`justify-self`** — overrides `justify-items` for one item; same value set: `start` | `end` | `center` | `stretch`.
9. **`align-self`** — overrides `align-items` for one item; same value set plus `baseline`.
10. **`place-self`** — shorthand for `align-self` + `justify-self`.
11. **`order`** — changes visual painting order without changing DOM order (also applies to flex items; interacts with Grid auto-placement).
12. **`z-index`** — resolves stacking when grid items are intentionally overlapped.

---

## 4. Grid Functions & Special Values

- **`repeat(count, track-list)`** — repeats a track pattern; `count` can be a number, `auto-fill`, or `auto-fit`.
- **`minmax(min, max)`** — sets a track's minimum and maximum size in one value; the classic responsive-track building block.
- **`fit-content(length)`** — clamps a track to the smaller of its content size or the given length.
- **`min()` / `max()` / `clamp()`** — general CSS math functions usable inside track sizing for fully fluid values without media queries.
- **`fr`** — the flexible fraction unit; distributes leftover space after fixed tracks/gaps.
- **`auto`** — track sizes to its content, up to available space.
- **`subgrid`** — used as a value for `grid-template-columns`/`grid-template-rows` on a nested grid item, inheriting the parent's tracks instead of defining new ones.
- **Named grid lines** — custom names in square brackets inside track definitions, e.g. `[sidebar-start] 240px [sidebar-end main-start] 1fr [main-end]`.
- **`masonry`** *(experimental)* — a proposed value for `grid-template-rows`/`columns` enabling Pinterest-style masonry layout; not Baseline-stable across all major browsers as of 2026 — check support before shipping.

---

## 5. Step-by-Step Internal Mechanics

1. The browser first resolves the **explicit grid** from `grid-template-columns`/`rows`.
2. Items with explicit `grid-row`/`grid-column` placements are positioned first.
3. Remaining items are auto-placed one by one, following `grid-auto-flow` (row-by-row by default).
4. If auto-placement runs out of explicit tracks, the browser generates **implicit tracks**, sized by `grid-auto-rows`/`columns`.
5. `dense` re-packs earlier empty cells with later items if they fit, which can reorder visual placement relative to DOM order.
6. Track sizes are resolved: fixed sizes first, then `minmax()`/content-based sizes, then remaining space is distributed to `fr` tracks.
7. Items are aligned within their resolved cell according to `justify-items`/`align-items`, or per-item overrides.
8. If the item is itself `subgrid`, its rows/columns are re-resolved directly against inherited parent tracks rather than repeating steps 1–6 independently.

---

## 6. Common Mistakes & Gotchas

- Forgetting the implicit **`min-width: auto`** / **`min-height: auto`** default on grid items, which lets long unbroken content overflow a fixed track — fix with `min-width: 0`.
- Confusing **`auto-fill`** (keeps empty tracks, items stay put) with **`auto-fit`** (collapses empty tracks, items stretch) — visually identical until the row isn't full.
- Assuming `fr` splits total container space evenly, ignoring that fixed-size tracks and gaps are subtracted first.
- Using `grid-template-areas` with an area name that doesn't form a rectangle — this is invalid and the declaration is dropped entirely.
- Overlapping items unintentionally because two `grid-area` placements resolve to the same lines.
- Forgetting `grid-auto-flow: dense` can visually reorder content ahead of DOM order — a real accessibility trap for keyboard and screen reader users.
- Nesting a nested grid without `subgrid` and expecting it to align with the parent's tracks automatically — it won't, they're independent grids.

---

## 7. Best Practices

- Default to `repeat(auto-fit, minmax(Npx, 1fr))` for content-driven responsive grids instead of manual breakpoints.
- Use named `grid-template-areas` for page-level layouts — it documents the layout visually in the CSS itself.
- Reach for `subgrid` for any nested component that must align cross-row with siblings it doesn't share a DOM parent-grid with.
- Pair Grid for macro-layout with Flexbox for micro-alignment inside individual cells.
- Prefer container queries over viewport media queries when a grid's responsiveness should depend on its own container, not the page.
- Always set an explicit `min-width: 0` (or `overflow` handling) on grid items containing unpredictable text content.
- Keep DOM order matching visual/reading order wherever possible, even when using `order` or `dense` for visual exceptions.

---

## 8. Anti-Patterns

- Using Grid with a single row or single column when Flexbox would be simpler and more idiomatic.
- Hardcoding a fixed number of `repeat(3, 1fr)` columns for genuinely unpredictable content counts instead of `auto-fit`/`auto-fill`.
- Using absolute positioning inside a grid cell to fake alignment Grid already handles natively.
- Recreating Bootstrap-style nested `.row > .col` wrapper divs when native `grid-template-columns` needs no wrapper structure at all.
- Using JavaScript to measure and sync heights across independent components instead of `subgrid`.
- Overusing `grid-auto-flow: dense` purely for visual "packing," breaking logical reading order for sighted-only aesthetic gain.

---

## 9. Grid vs Related Concepts

| | **CSS Grid** | **Flexbox** | **Table layout** | **Masonry (experimental)** |
|---|---|---|---|---|
| Dimensions | Two (rows + columns) | One (main axis, cross axis is secondary) | Two, but row-height-locked | Two, but items don't align in a strict grid |
| Best for | Page layouts, dashboards, card grids | Nav bars, button groups, single-direction distribution | Genuine tabular data | Pinterest-style variable-height galleries |
| Alignment control | Full 2D control via lines/areas | Strong 1D control, weak cross-axis control | Rigid, row-locked | Column-locked, row-flexible |
| 2026 status | Baseline, fully stable, subgrid supported everywhere | Baseline, fully stable | Baseline (semantic use only) | Not Baseline-stable across all engines |

---

## 10. Performance Implications

- Grid recalculation is triggered by container resize, content changes, or added/removed items — same reflow cost category as Flexbox, not inherently more expensive.
- Deeply nested grids (grid inside grid inside grid) increase layout computation cost linearly with nesting depth; `subgrid` avoids adding a full independent layout pass.
- `auto-fit`/`auto-fill` with `minmax()` recalculates track counts on every resize — negligible for typical UIs, but worth profiling in data-dense tables with thousands of rows.
- Avoid triggering layout thrash by reading computed grid dimensions via JS (`getBoundingClientRect`) inside a resize loop instead of relying on container queries.

---

## 11. Browser & Runtime Support Notes (2026)

- Core Grid (`display: grid`, template properties, `fr`, `minmax()`, `repeat()`) — Baseline, fully supported in all evergreen browsers since 2020.
- **Subgrid** — Baseline across Firefox, Chrome/Chromium, Safari since 2023; safe for production use without fallbacks in any evergreen-browser-targeted product.
- **Container queries** — Baseline since 2023; safe to use as the default responsive strategy for component-level layout.
- **Masonry value** (`grid-template-rows: masonry`) — still experimental/behind-flag in some engines; do not ship without a fallback or feature detection.
- No meaningful support gap remains for standard Grid in any product targeting current evergreen browsers — legacy `-ms-grid` prefixed syntax (old Edge) is dead and should never appear in new code.

---

## 12. Accessibility Implications

- Visual reordering via `order` or `grid-auto-flow: dense` does **not** change DOM order, which is what screen readers and keyboard `Tab` navigation follow — a mismatch here creates a genuinely confusing experience for assistive tech users.
- Keep source order matching logical reading order; use visual-only reordering sparingly and test with keyboard navigation, not just sighted review.
- Grid layout itself carries no special ARIA requirements — semantics come from the underlying HTML elements, not the layout mechanism.
- Overlapping content (intentional layering) must maintain sufficient contrast and not obscure focus indicators for interactive elements underneath.

---

## 13. Security Implications

- CSS Grid carries no direct security surface on its own, but dynamically injected `grid-template-columns`/`areas` values built from unsanitized user input in a CSS-in-JS or inline `style` context can enable CSS injection in edge cases — treat any user-controlled style value the same as any other unsanitized string.
- Avoid interpolating raw user input directly into `style` attributes or template literals feeding styled-components/CSS variables without validation.

---

## 14. Quick Code Reference

```css
/* Responsive card grid, no media queries */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.5rem;
}

/* Named-area page layout */
.layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
}

/* Subgrid for cross-component row alignment */
.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3;
}

/* Container query driven internal grid */
.card { container-type: inline-size; }
@container (min-width: 400px) {
  .card-grid { grid-template-columns: 1fr 1fr; }
}
```

---

## 15. Rapid-Fire Interview One-Liners

- Grid is two-dimensional; Flexbox is one-dimensional with a secondary axis.
- `fr` divides *leftover* space, not total space.
- `auto-fit` collapses empty tracks; `auto-fill` preserves them.
- Grid items default to `min-width: auto`, which can cause overflow on fixed tracks.
- `subgrid` lets a nested grid inherit parent tracks — Baseline since 2023.
- `grid-auto-flow: dense` can visually reorder content ahead of DOM order — an accessibility risk.
- Named `grid-template-areas` must form valid rectangles or the whole rule is invalid.
- Container queries make component-level responsiveness possible without JS or page-level media queries.
- Grid rows auto-stretch to the tallest item by default — free equal-height columns.
- Explicit grid = what you define; implicit grid = what the browser invents when content overflows it.

---

## 16. In React/Next.js Projects

- Dynamic `grid-template-columns` computed from server data must be deterministic across server render and client hydration in Next.js Server Components — pass the value as a prop and apply it via a CSS custom property, not a freshly recomputed inline style object.
- Tailwind's `grid-cols-*` utilities are statically generated at build time — a template-literal class like `` `grid-cols-${n}` `` compiles to nothing; use arbitrary-value syntax (`grid-cols-[repeat(var(--cols),1fr)]`) or a CSS Module for truly dynamic column counts.
- Reusable layout components (design systems, component libraries) should expose track sizing via CSS custom properties with sensible defaults, not hardcoded pixel values, so consuming teams can override without forking the component.
- A grid-based component that looks correct in isolation but misaligns when reused under a different parent is almost always a cross-component alignment problem — fix with `subgrid` if the parent is also a grid, or container queries if it should respond to its own available width.
- `grid-auto-flow: dense` combined with client-side reordering (drag-and-drop dashboards) needs care in React: update the underlying data/state driving placement, not DOM order directly, or you'll fight React's reconciliation.
- CSS Modules and Tailwind can be combined safely for Grid — use Tailwind for standard track patterns, drop to a CSS Module or inline custom property for anything genuinely dynamic or data-driven.

---

## 17. In the AI Era

- AI assistants frequently default to rigid `repeat(3, 1fr)` plus three separate media-query breakpoints instead of `auto-fit`/`minmax()` — the older, higher-maintenance pattern is overrepresented in training data relative to newer idioms.
- Assistants often generate `auto-fill` when the actual visual requirement was `auto-fit` (items stretching to fill the row) — this bug is visually invisible until the row isn't completely full, so it passes a quick glance and even a screenshot-based review.
- Subgrid and container queries are rarely reached for unless named explicitly in the prompt — you need to already know these techniques exist to prompt for them correctly.
- AI-generated dynamic Tailwind class strings (e.g. template-literal `grid-cols-${n}`) are a recurring subtle bug, since the assistant doesn't account for Tailwind's static build-time class generation.
- AI-written layout code rarely accounts for the implicit `min-width: auto` overflow trap, producing grids that "work" in the demo but break the moment real, unpredictable content (long strings, filenames, URLs) is dropped in.
- What you must verify manually: whether the chosen sizing function (`auto-fit` vs `auto-fill`, fixed vs `fr`, media query vs container query) actually matches the stated design intent — an assistant can produce valid syntax without ever confirming it matches what you meant.
- This topic doesn't become obsolete with AI assistance because reviewing generated layout code is a comprehension task, not a typing task — you're judging design intent, edge-case behavior, and idiomatic currency, none of which the assistant verifies on its own.
