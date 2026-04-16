# Cat Collector — Dev Notes

## Layout Architecture (hard-won lessons)

### Vertical stack in `#app` (flex column)
```
#header     — position:sticky, flex-shrink:0
#main       — flex:1, centers ONLY the tap button
#cat-mood   — flex-shrink:0, own strip between main and ad-bar
#ad-bar     — flex-shrink:0
#shop       — height:40vh, flex-shrink:0
```

### Critical rules
- **`#main` must NOT have `overflow:hidden`** — it clips the tap button's box-shadow glow upward, making it look like it's behind the header.
- **`#cat-mood` must live OUTSIDE `#main`** — if it's inside, `justify-content:center` groups it with the button and pushes the button toward the header.
- **`#header` is `position:sticky`** (not fixed) so it participates in normal flow and `#main` starts correctly below it. `#app` has `overflow:hidden` which disables scrolling.
- **`#tap-btn` sizing**: `min(200px, 42vw, 28vh)` — the `28vh` constraint keeps it from being too large on short screens (iPhone SE).
- **`#main` bottom padding** (`padding-bottom:18px`) creates visual separation between ticker text and the mood bars below.

### Small screen media query
```css
@media (max-height:700px) {
  #shop { height:34vh; }
  #tap-hint, #ticker { display:none; }
}
```
Hides flavor text and shrinks shop on iPhone SE to give the button enough room.
