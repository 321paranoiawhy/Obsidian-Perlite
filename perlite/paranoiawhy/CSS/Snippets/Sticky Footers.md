---
tags: CSS, Snippets, Sticky-Footers
---
# Flexbox

[[Auto Numbering Elements]]

## 利用 flex 相关属性

```html
<div class="container">
  <header></header>
  <main></main>
  <footer></footer>
</div>
```

```css
.container {
	min-height: 100%;
	display: flex;
}

main {
	flex: 1 0 auto;
	/*   flex-grow: 1;
	flex-shrink: 0;
	flex-basis: auto; */
}

header,footer {
	flex-shrink: 0;
}
```

## 利用 margin-top: auto

```css
.container {
	min-height: 100%;
	display: flex;
}

header, main, footer {
	flex-shrink: 0;
}

footer {
	margin-top: auto;
}
```

# `Grid`

# Reference

- [Sticky footers - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Layout_cookbook/Sticky_footers)
- [Sticky Footer, Five Ways](https://css-tricks.com/couple-takes-sticky-footer/)
- [Sticky Footer Solved by Flexbox](https://philipwalton.github.io/solved-by-flexbox/demos/sticky-footer/)
- [Sticky footer - getbootstrap](https://getbootstrap.com/docs/5.3/examples/sticky-footer/)
- [前端 CSS 如何实现 Footer 置底？](https://www.zhihu.com/question/587667634/answer/2923946795?utm_source=wechat_session&utm_medium=social&utm_oi=1071532971839766528)