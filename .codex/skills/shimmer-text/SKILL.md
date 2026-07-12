---
name: shimmer-text
description: Use this skill when creating, explaining, or adapting a CSS shimmer text effect with gradient text, background clipping, safe travel distance, and smooth restart/pause controls.
---

# Shimmer Text

Use this workflow to build a readable CSS shimmer text effect.

## Core Idea

The text does not move. A larger gradient background moves behind the text, and `background-clip: text` reveals only the part of that background inside each glyph.

## Minimal DOM

```html
<p class="shimmer">CSS is awesome, right?</p>
```

## Base CSS

```css
.shimmer {
  --speed: 2.4s;
  --angle: 45deg;
  --shine-width: 120px;
  --start-position: 72%;
  --end-position: 28%;

  color: transparent;
  background-image: linear-gradient(
    var(--angle),
    #8a8a8a calc(50% - var(--shine-width)),
    #ffffff 50%,
    #8a8a8a calc(50% + var(--shine-width))
  );
  background-size: 400% 100%;
  background-position: var(--start-position) 0;
  background-clip: text;
  -webkit-background-clip: text;
  animation: shimmer var(--speed) ease-in-out infinite both;
}

@keyframes shimmer {
  0% {
    background-position: var(--start-position) 0;
  }

  72%,
  100% {
    background-position: var(--end-position) 0;
  }
}
```

## Implementation Checklist

1. Start with plain readable text.
2. Add a static gradient using `background-image`, not `background`, if other background longhands need to be preserved.
3. Set `color: transparent`, `background-clip: text`, and `-webkit-background-clip: text`.
4. Increase `background-size`, commonly `400% 100%`, so the highlight has space to enter and leave.
5. Animate `background-position`.
6. Keep a short hold at the end of the keyframes, for example `72%, 100%`, so the loop has a smooth finish.

## Safe Travel Distance

When the highlight is angled, it needs extra horizontal travel before it touches the text. Estimate that margin from the highlight width, text height, and angle:

```js
const angle = 45 * Math.PI / 180;
const safeDistance =
  (shineWidth + textHeight * Math.abs(Math.cos(angle)) / 2)
  / Math.abs(Math.sin(angle));
```

Use this value to push the start and end positions outward so restart begins outside the first visible letter.

## Quality Notes

- Keep the highlight narrow for a premium shimmer, often around `2ch`.
- Use `ease-in-out` for gentle entry and exit.
- Restart by temporarily setting `animation: none`, forcing a reflow, then restoring the animation.
- For teaching demos, show three overlays: visible text range, calculated safe range, and full background highlight.
