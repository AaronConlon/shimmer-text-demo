# Shimmer Text Demo

这是一个交互式 CSS shimmer text 教学 demo。页面展示了最终效果、完整高亮背景、文字可见范围、计算后的安全移动范围，并用分步教程解释每一段代码是如何组合起来的。

线上预览：https://aaronconlon.github.io/shimmer-text-demo/

默认英文 README：[README.md](README.md)

## 这个 Demo 教什么

- 使用 `linear-gradient()` 创建高亮色带。
- 使用 `background-clip: text` 把背景裁剪进文字形状。
- 让背景比文字更宽，确保高亮可以从文字外进入，再从文字外离开。
- 根据高亮宽度和角度计算安全距离。
- 动画移动的是 `background-position`，不是文字本身。

## 核心 CSS

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

## 本地运行

这是一个静态页面。你可以直接打开 `index.html`，也可以用任意静态服务器启动：

```bash
npx serve .
```

## 仓库内置 Skill

仓库提供了一个 Codex 风格的 skill：

```text
.codex/skills/shimmer-text/SKILL.md
```

当你想让 agent 在其他项目里复刻或改造 shimmer text 效果时，可以使用它。

## 作者

Built by [Aaron Conlon](https://x.com/intent/follow?screen_name=aaronconlondev).
