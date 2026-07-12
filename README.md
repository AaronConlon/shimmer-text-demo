# Shimmer Text Demo

An interactive visual guide for building a CSS shimmer text effect. It shows the final demo, the oversized moving background, the visible text range, and a step-by-step tutorial with highlighted code.

Live preview: https://aaronconlon.github.io/shimmer-text-demo/

Chinese README: [README.zh-CN.md](README.zh-CN.md)

## What This Demonstrates

- Create a highlight with `linear-gradient()`.
- Clip the gradient into the text with `background-clip: text`.
- Make the background wider than the text so the highlight can enter and leave cleanly.
- Use a calculated safe distance based on highlight width and angle.
- Animate `background-position`, not the text itself.

## Core CSS

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

## Run Locally

This is a static page. You can open `index.html` directly, or serve it with any static server:

```bash
npx serve .
```

## Repository Skill

This repo includes a Codex-style skill at:

```text
.codex/skills/shimmer-text/SKILL.md
```

Use it when you want an agent to recreate or adapt the shimmer text effect in another project.

## Credits

Built by [Aaron Conlon](https://x.com/intent/follow?screen_name=aaronconlondev).
