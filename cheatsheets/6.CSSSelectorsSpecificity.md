# The Complete Reference: Selectors, Specificity & the Cascade
**Pillar:** Foundations Done Right — HTML & CSS · **Level:** Advanced
*Keep this open while coding, refactoring cascade bugs, or doing final interview prep.*

---

## 1. Core Definitions & Vocabulary

- **Selector** — a pattern used to match one or more elements in the document, so a rule's declarations apply to them.
- **The cascade** — the algorithm the browser runs to resolve which of several matching, conflicting declarations actually applies to an element.
- **Specificity** — a three-part weight assigned to a selector, used as one specific stage within the cascade (not the whole algorithm).
- **Origin** — which "source" a stylesheet comes from: user-agent, user, or author. Origin is resolved before specificity.
- **Importance** — whether a declaration is marked `!important`, which changes its priority within its origin.
- **Cascade layer (`@layer`)** — a named or anonymous priority bucket for author styles; layer order overrides specificity between layers.
- **Computed value / used value** — the value assigned after the cascade resolves, inheritance is applied, and any remaining relative values are computed.
- **Inheritance** — separate from the cascade: some properties (e.g. `color`, `font-family`) pass down to descendants by default if unset, regardless of cascade outcome.
- **Shadow DOM boundary** — a scoping boundary that most selectors cannot cross, requiring `::part()`, `::slotted()`, or `:host()` to style across it.

---

## 2. The Full Cascade Resolution Order (Step-by-Step Mechanics)

The browser evaluates conflicting declarations targeting the same element and property in this exact order — each stage only runs if the previous stage ends in a tie:

1. **Origin & Importance** — user-agent normal → user normal → author normal → CSS animations → author `!important` → user `!important` → user-agent `!important` → transition origin (highest of all).
2. **Cascade Layers** — declarations in a later-declared layer beat declarations in an earlier-declared layer, regardless of specificity. Unlayered author CSS is treated as an implicit final layer (highest of all named layers).
3. **Specificity** — the three-column (ID, class/attribute/pseudo-class, type/pseudo-element) comparison, evaluated lexicographically, left to right.
4. **Source Order** — if everything above ties, the declaration that appears later in the document/stylesheet, or was inserted later at runtime, wins.

> **Key mental model correction:** specificity is stage 3 of 4. Layers sit *above* specificity, and origin/importance sits above layers. This is why `!important` and layer placement can each independently override "the more specific selector wins."

---

## 3. Selector Syntax — Full Surface

### Combinators
| Combinator | Syntax | Meaning |
|---|---|---|
| Descendant combinator | `A B` | B is any descendant of A |
| Child combinator | `A > B` | B is a direct child of A |
| Adjacent sibling combinator | `A + B` | B is immediately preceded by sibling A |
| General sibling combinator | `A ~ B` | B is any later sibling of A |
| Column combinator *(experimental, table columns)* | `A \|\| B` | B belongs to column A |

### Simple Selectors
| Selector | Syntax | Meaning |
|---|---|---|
| Universal selector | `*` | Matches any element |
| Type selector | `div`, `p`, `section` | Matches by tag name |
| Class selector | `.card` | Matches elements with that class |
| ID selector | `#header` | Matches the element with that ID |
| Selector list | `a, b, c` | Matches any element matching any listed selector |

### Attribute Selectors
| Syntax | Meaning |
|---|---|
| `[attr]` | Has the attribute, any value |
| `[attr=value]` | Exact value match |
| `[attr~=value]` | Value appears as one word in a space-separated list |
| `[attr\|=value]` | Value equals, or starts with value followed by a hyphen |
| `[attr^=value]` | Value starts with |
| `[attr$=value]` | Value ends with |
| `[attr*=value]` | Value contains |
| `[attr=value i]` | Case-insensitive match modifier |
| `[attr=value s]` | Case-sensitive match modifier (explicit) |

---

## 4. Pseudo-Classes — Full Enumeration

**Link / user action**
- `:link` — unvisited link
- `:visited` — visited link (style access heavily restricted for privacy)
- `:hover` — pointer is over the element
- `:active` — element is being activated (e.g. mid-click)
- `:focus` — element has focus
- `:focus-visible` — element has focus *and* the UA determines focus should be visibly indicated (keyboard nav, typically)
- `:focus-within` — element or any descendant has focus

**Location / target**
- `:target` — element is the target of the current URL fragment
- `:target-within` — element or a descendant is the fragment target
- `:current`, `:past`, `:future` — media/cue timeline pseudo-classes (used with WebVTT-style timed content)

**Input / form state**
- `:enabled` / `:disabled`
- `:checked` — checked checkbox/radio/option
- `:indeterminate` — indeterminate checkbox or `<progress>` without a value
- `:default` — the default option/button in a group
- `:required` / `:optional`
- `:valid` / `:invalid`
- `:in-range` / `:out-of-range`
- `:read-only` / `:read-write`
- `:placeholder-shown`
- `:user-valid` / `:user-invalid` — validity state, but only after meaningful user interaction (avoids validating untouched fields)
- `:autofill` — field currently showing browser-autofilled value

**Structural**
- `:root` — the document's root element
- `:empty` — element with no children (including no text nodes)
- `:first-child` / `:last-child` / `:only-child`
- `:first-of-type` / `:last-of-type` / `:only-of-type`
- `:nth-child(An+B [of S])` / `:nth-last-child(An+B [of S])` — supports the `of <selector>` filtered syntax
- `:nth-of-type(An+B)` / `:nth-last-of-type(An+B)`

**Logical / combinator-style**
- `:not(<selector list>)`
- `:is(<selector list>)` — matches if any argument matches; takes the specificity of its most specific argument
- `:where(<selector list>)` — same matching behavior as `:is()`, but always contributes zero specificity
- `:has(<relative selector list>)` — matches if the given relative selector matches something inside/after it (the only native "parent selector")

**Language / direction**
- `:lang(code)`
- `:dir(ltr | rtl)`

**Fullscreen / overlay / popover**
- `:fullscreen`
- `:modal`
- `:picture-in-picture`
- `:popover-open`

**Custom elements / Shadow DOM**
- `:defined` — custom element has been defined (upgraded)
- `:host` — matches the shadow host from inside its shadow tree
- `:host(<selector>)` — matches the host only if it also matches the given selector
- `:host-context(<selector>)` — matches the host if it, or an ancestor, matches the given selector
- `:state(name)` — matches a custom element exposing a given custom state via `ElementInternals`

**Scoping**
- `:scope` — matches the reference point for a selector (e.g. the anchor of `@scope`, or a query's context node)

---

## 5. Pseudo-Elements — Full Enumeration

- `::before` / `::after` — generated content boxes
- `::first-line` — first formatted line of a block
- `::first-letter` — first letter/symbol of a block
- `::selection` — user-highlighted text
- `::placeholder` — placeholder text of a form field
- `::marker` — the marker box of a list item or `<summary>`
- `::backdrop` — the backdrop rendered behind a top-layer element (`<dialog>`, fullscreen elements, popovers)
- `::file-selector-button` — the button part of `<input type="file">`
- `::part(name)` — an element inside a shadow tree explicitly exposed via `part` attribute
- `::slotted(selector)` — a light-DOM element projected into a `<slot>`
- `::cue` / `::cue(selector)` — WebVTT text track cues
- `::grammar-error` / `::spelling-error` — UA-flagged text issues
- `::target-text` — text fragment matched via a URL text-fragment link
- `::highlight(name)` — text ranges registered via the `CSS.highlights` Highlight API
- `::view-transition`, `::view-transition-group()`, `::view-transition-image-pair()`, `::view-transition-old()`, `::view-transition-new()` — View Transitions API pseudo-element tree
- `::details-content` *(experimental, not yet Baseline)* — the expandable content box of `<details>`
- `::picker(select)` *(experimental, not yet Baseline)* — the drop-down picker part of a customizable `<select>`
- `::picker-icon` *(experimental, not yet Baseline)* — the dropdown arrow icon of a customizable form control
- `::checkmark` *(experimental, not yet Baseline)* — the selection checkmark inside an `<option>` of a customizable `<select>`

> **Note:** the customizable-`<select>` pseudo-elements (`::picker`, `::picker-icon`, `::checkmark`, `::details-content`) are real, shipping-in-some-browsers features as of 2026 but are **not yet Baseline** — verify support before relying on them in production.

---

## 6. Specificity — Calculation Rules

- Specificity is a **3-column tuple**: `(ID count, class/attribute/pseudo-class count, type/pseudo-element count)`.
- Columns are compared **left to right, lexicographically** — never summed into one number.
- The universal selector `*`, combinators (`>`, `+`, `~`, ` `), and `:where()` contribute **zero** specificity.
- `:not()`, `:is()` contribute the specificity of their **most specific argument**, not a flat +1.
- `:has()` contributes the specificity of its most specific argument, same rule as `:is()`.
- Native CSS nesting: the parent selector context is folded in similarly to an implicit `:is()`, so nested rules inherit the parent chain's specificity even when the nested line looks minimal.
- `!important` does **not** change specificity — it changes origin/importance priority, a separate, earlier stage.
- Inline `style="..."` attributes are stronger than any selector-based specificity (conceptually a 4th, higher column) but weaker than an author `!important`.

**Worked comparisons:**
```
#id                     → 1-0-0
.class.class.class      → 0-3-0   (loses to any single ID selector)
div.class                → 0-1-1
:where(#id) .class       → 0-1-0   (the ID inside :where() is neutralized)
:is(#id, .class) span    → 1-0-1   (inherits the ID's weight from :is())
```

---

## 7. Cascade Layers — Syntax Reference

```css
/* Declare layer order up front — order here is what matters, not declaration position later */
@layer reset, base, components, utilities;

@layer base {
  body { line-height: 1.5; }
}

@layer components {
  .btn { padding: 8px 16px; }
}

/* Nested/sub-layers */
@layer components.buttons {
  .btn--primary { background: blue; }
}

/* Anonymous layer — still ordered by position, but not addressable by name elsewhere */
@layer {
  .temp-override { color: red; }
}

/* Importing a stylesheet directly into a named layer */
@import url("vendor.css") layer(vendor);
```

- Layers declared later always win over layers declared earlier, **regardless of specificity**.
- A layer's *priority* is fixed by where it's first declared (e.g. the `@layer reset, base, components, utilities;` statement) — you can add more rules to an earlier layer later in the file without it moving up in priority.
- Unlayered rules are always the highest-priority "layer," beating every named layer.
- `!important` **reverses** layer order: an `!important` declaration in an *earlier* layer beats an `!important` declaration in a later layer.

---

## 8. `:is()` vs `:where()` vs `:has()` — Direct Comparison

| Feature | `:is()` | `:where()` | `:has()` |
|---|---|---|---|
| Matching logic | Matches if any argument matches | Matches if any argument matches | Matches if a relative selector matches inside/after |
| Specificity contributed | Highest of its arguments | Always zero | Highest of its arguments |
| Typical use case | Grouping selectors concisely | Grouping without specificity cost (libraries, resets) | Parent/ancestor-based conditional styling |
| Forgiving selector list | Yes (Level 4 UAs skip invalid args) | Yes | Yes |

---

## 9. Common Mistakes & Gotchas

- Assuming specificity is the whole cascade algorithm and ignoring origin/importance and layers entirely.
- Treating `.a.b.c` as "specificity 3" instead of understanding it's `0-3-0` and still loses to any single ID.
- Not knowing unlayered CSS silently outranks every named `@layer`, regardless of specificity.
- Assuming `:is()` and `:where()` are interchangeable — swapping them changes real override behavior.
- Underestimating nested selectors' true specificity because the nested line looks shallow.
- Reaching for `!important` as a first fix instead of diagnosing which of the four stages is actually responsible.
- Forgetting that `!important` **inverts** layer priority order, causing "wait, why did the earlier layer win?" confusion.
- Assuming visited-link styling can be read back via JavaScript or fully styled like any other state — browsers deliberately restrict this for privacy.

---

## 10. Best Practices

- Declare your full `@layer` order once, near the top of your global stylesheet, before any layer contains rules.
- Use `:where()` for any selector meant to be easily overridden by consumers (libraries, design systems, resets).
- Prefer flat, low-specificity selectors for app-level styling; reserve high specificity for deliberate, rare overrides.
- Treat `!important` as an escape hatch for overriding third-party/generated CSS you don't control — not routine styling.
- Keep utility classes (Tailwind-style) in their own dedicated layer, ordered last, so their override intent is explicit and durable.
- Document any nesting that pulls in a highly specific parent context, since it's not visually obvious from the nested line alone.

---

## 11. Anti-Patterns

- ID selectors used purely for styling hooks (not just unique DOM anchors) — creates specificity that's hard to override later.
- Stacking extra classes (`.a.b.c.d`) purely to "win" a cascade fight instead of restructuring layers or specificity intentionally.
- Sprinkling `!important` across a codebase as a general-purpose override tool.
- Mixing layered and unlayered author CSS without a team convention — guarantees accidental unlayered overrides.
- Deeply nesting selectors purely for visual code organization without considering the specificity that gets folded in.

---

## 12. Comparisons vs Related Concepts

- **Cascade vs inheritance** — the cascade picks *which declaration* applies; inheritance is a separate fallback that only applies to specific properties when no declaration set a value at all.
- **Specificity vs source order** — specificity is stage 3; source order is stage 4 and only matters once specificity ties.
- **`@layer` vs specificity restructuring** — layers set priority *architecturally, once*; specificity restructuring is a per-rule, ongoing negotiation.
- **Inline styles vs authored CSS** — inline styles behave like a stronger authority than any selector-based specificity, but are still beaten by an authored `!important`.
- **CSS Modules vs utility-first CSS** — CSS Modules change class *names* (scoping) but not cascade weight; utility-first frameworks equalize specificity and shift the real conflict resolution to generated stylesheet order.

---

## 13. Performance Implications

- Selector matching cost in modern engines is dominated by the **rightmost (key) selector** and how many candidate elements it matches — overly broad key selectors (e.g. `* .item`) force more matching work.
- Extremely long selector lists or deeply chained `:not()`/`:is()`/`:has()` combinators increase style recalculation cost, particularly `:has()`, which can require looking at descendants/siblings rather than just ancestors.
- Cascade layers do not meaningfully change per-rule matching performance — they change resolution priority, not selector matching cost.
- Runtime CSS-in-JS that injects/re-injects style tags on every render (rather than once) can cause unnecessary style recalculation and layout thrashing — a performance issue caused by cascade mechanics, not just React re-renders.

---

## 14. Browser / Runtime Support Notes (as of 2026)

- Cascade layers (`@layer`), `:is()`, `:where()`, `:has()`, and native CSS nesting are all Baseline-widely-available across evergreen browsers.
- `:user-valid` / `:user-invalid` are Baseline and safe to use for form UX without polyfills.
- Customizable `<select>` pseudo-elements (`::picker()`, `::picker-icon`, `::checkmark`, `::details-content`) are shipping in some engines but **not yet Baseline** — feature-detect or progressively enhance rather than relying on them universally.
- The column combinator (`||`) remains experimental/unevenly supported — avoid it in production selectors.

---

## 15. Security Implications

- `:visited` styling is intentionally limited by browsers (restricted property list, no JS introspection) to prevent history-sniffing attacks — don't rely on `:visited` for anything beyond basic link color changes.
- User-generated content rendered with `dangerouslySetInnerHTML` (React) or raw HTML injection can carry inline `style` attributes or `<style>` tags that hijack the cascade for the surrounding page — sanitize or strip style-related attributes/tags from untrusted HTML.
- Overly permissive attribute selectors combined with user-controlled class/attribute values can be used to fingerprint or leak state via style-based side channels in unusual cases — avoid binding security-sensitive logic to CSS state.

---

## 16. Accessibility Implications

- `:focus-visible` should be preferred over `:focus` for visible focus rings, so mouse users aren't shown rings meant for keyboard navigation, while keyboard users still reliably get them.
- Removing focus indicators via aggressive specificity or `!important` overrides (common when "cleaning up" browser default styles) is a frequent, serious accessibility regression — always verify focus visibility survives your cascade.
- `:has()` enables accessible patterns like styling a `<label>` based on its associated input's `:invalid` state without JavaScript, reducing the need for extra ARIA-live wiring.
- `::marker` and `::placeholder` styling should preserve sufficient color contrast — these are easy to visually deprioritize into low-contrast, hard-to-read states.

---

## 17. Quick Code Example — Everything in One Place

```css
@layer reset, base, components, utilities;

@layer base {
  body { color: #111; }
}

@layer components {
  :where(.card) {
    padding: 24px;             /* 0-0-0 specificity — easily overridable */
  }
  .card:has(> .card__error) {
    border-color: red;         /* :has() for parent-based state, no JS */
  }
}

@layer utilities {
  .p-0 { padding: 0; }         /* wins over .card's padding — later layer */
}

/* Unlayered — outranks every layer above, use sparingly and deliberately */
.debug-outline { outline: 2px solid magenta; }
```

---

## 18. Rapid-Fire Interview One-Liners

- Specificity is stage 3 of a 4-stage cascade algorithm — origin/importance and layers both outrank it.
- `!important` wins by origin, not specificity — that's why it can beat a "more specific" selector.
- `:where()` = zero specificity, always. `:is()` = specificity of its strongest argument.
- Unlayered CSS is treated as the highest-priority implicit layer.
- Layer order is fixed by the *first* declaration of the layer order, not by where rules are physically added later.
- Native nesting folds the parent selector into specificity — nested rules aren't as "light" as they look.
- Source order is the *weakest* signal — it only matters once everything else is tied.
- `!important` inverts priority *between* layers, but not within origin/importance overall.
- `:has()` is the only native way to select based on descendants — it's a real "parent selector."
- Inline styles beat any selector-based specificity but still lose to an authored `!important`.

---

## In React/Next.js Projects

- **CSS Modules and specificity are unrelated concerns** — scoped class name hashing changes *names*, not cascade weight; two CSS Modules can still collide on the same property with unpredictable winner based on bundler output order.
- **Import order ≠ render order** — in the Next.js App Router, which CSS Module ends up first in the compiled stylesheet depends on the bundler's module graph, which can differ between local dev and a production build.
- **Runtime CSS-in-JS injection races** — styled-components/Emotion inject `<style>` tags at render time; with Suspense-based streaming SSR, sibling components can render (and inject styles) in a different order than expected, creating source-order cascade bugs that look flaky.
- **Tailwind utilities are internally layered** — conflicting utility classes in the same `className` string are resolved by Tailwind's generated `@layer utilities` stylesheet order, not by the order you typed the class names in JSX.
- **Global CSS + CSS Modules interplay** — a global stylesheet imported in a Next.js root layout and a component's CSS Module can conflict; whichever is unlayered (commonly the global file) can unexpectedly outrank scoped module styles.
- **Design-system/component-library authoring** — internal library selectors should use `:where()` so consuming app teams can override with a plain class instead of needing `!important` or ID-level specificity.
- **`:has()` replacing JS-driven conditional class logic** — patterns like "style a form row differently if its input is invalid" can now be done with `.row:has(:invalid)` instead of tracking validity state in React just to toggle a class.
- **Next.js layout-level CSS ordering** — styles imported in a nested layout can be inserted after a parent layout's styles in the compiled output, meaning "more specific" component styles can still lose if the parent layout's CSS is unlayered and loads later.

---

## In the AI Era

- **Default failure pattern:** when a style "isn't applying," AI assistants (Copilot, Cursor, Claude Code, etc.) frequently patch it by adding `!important` or an extra wrapper class to inflate specificity — winning at origin or specificity while leaving the real root cause (a layer conflict, an unlayered override, an injection-order race) completely undiagnosed.
- **Why this happens structurally:** diagnosing a cascade conflict requires visibility into the entire project's `@layer` order, bundler import graph, and every other rule that could match the same element — context that isn't available within a single file or prompt scope, unlike a typical local logic bug.
- **Subtle bugs AI tools introduce:** generated components that nest selectors under a highly specific parent without realizing the inherited specificity now silently outranks unrelated rules elsewhere in the codebase.
- **Subtle bugs in CSS-in-JS suggestions:** AI-suggested styled-components/Emotion code that doesn't account for Suspense/streaming render-order effects on style injection timing, producing "works in this one test, breaks under load" bugs.
- **What you must manually verify in review:** whether a new or modified rule is placed inside the correct existing `@layer`, or slipped in unlayered and now silently outranks the whole system.
- **What you must manually verify in review:** whether an `!important` the assistant added is masking a root cause (layer/order/specificity) that will resurface as a harder bug for the next contributor.
- **What you must manually verify in review:** whether nested selectors the assistant generated inherit more specificity from context than the flat, visible line suggests.
- **How to prompt better:** instead of "make this override work," specify cascade intent directly — "add this inside our existing `components` layer," "use `:where()` since this must be overridable," "don't use `!important`."
- **Why this doesn't become obsolete:** an AI assistant can produce syntactically valid CSS in seconds, but only a developer who understands the four-stage cascade can judge whether that "working" fix actually preserved — or quietly broke — the architecture's override guarantees for everyone downstream.
