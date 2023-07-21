## 顶部滚动进度

### HTML + CSS + JS

`HTML`:

```html
<progress id='scroll-progress' value='0'></progress>
```

`CSS`:

```css
#scroll-progress {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 1000;
  width: 100%;
  height: 2px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border: none;
  background-color: transparent;
  --progress-color: #ff5d52;
}
#scroll-progress::-webkit-progress-bar {
  background-color: transparent;
}
#scroll-progress::-webkit-progress-value {
  background-color: var(--progress-color);
}
#scroll-progress::-moz-progress-bar {
  background-color: var(--progress-color);
}
```

`JS`:

```js
document.addEventListener("DOMContentLoaded", () => {
  const winHeight = window.innerHeight,
    docHeight = document.documentElement.scrollHeight,
    progressBar = document.querySelector("#scroll-progress");
  progressBar.max = docHeight - winHeight;
  progressBar.value = window.scrollY;

  document.addEventListener("scroll", () => {
    progressBar.max =
      document.documentElement.scrollHeight - window.innerHeight;
    progressBar.value = window.scrollY;
  });
});
```

### Scroll-Driven

- [animation-timeline - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timeline)
- [scroll-driven-animations.style](https://scroll-driven-animations.style/)
- [Scroll-driven animations](https://developer.chrome.com/articles/scroll-driven-animations/)

`HTML`:

```html
<div id='scroll-progress'></div>
```

`CSS`:

```css
@keyframes grow-progress {
  from {
    transform: scaleX(0);
  }
  to {
    transform: scaleX(1);
  }
}

#scroll-progress {
  animation: grow-progress auto linear forwards;
  animation-timeline: scroll(block root);
  transform-origin: 0 50%;
  transform: scaleX(0);
}

/* 定位及样式 */
#scroll-progress {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  width: 100%;
  height: 2px;
  background-color: red;
}
```

[Codepen](https://codepen.io/paraoiawhy/pen/poQaaze)

上述 `CSS` 代码也可使用 `JS` 实现:

```js
const progressBar = document.querySelector('#scroll-progress');

progressBar.style.transformOrigin = '0% 50%';

progressBar.animate(
  {
    transform: ['scaleX(0)', 'scaleX(1)'],
  },
  {
    fill: 'forwards',
    timeline: new ScrollTimeline({
      source: document.documentElement,
    }),
  }
);
```

## 实时显示滚动进度

### Scroll-Driven

`HTML`:

```html
<div class="scroller">
  <div class="scroller-content"></div>
  <div class="scroll-progress">0%</div>
</div>
```

`CSS`:

```css
.scroller {
  scroll-timeline: --the-scroller;

  border: var(--scrollbox-border-size) solid lightblue;
  box-sizing: border-box;
  height: calc(100vh - 2em);
  width: var(--scrollbox-width);
  overflow: auto;
  max-width: 90vw;
  margin: 0 auto;
  position: relative;
  box-shadow: inset 0px 0px 1em 0px rgb(0 0 0 / 0.5),
    0px 0px 1em 0px rgb(0 0 0 / 0.5);
  border-radius: 0.5em;
}

.scroll-progress {
  position: fixed;
  inset: 0;
  display: grid;
  place-content: center;
  pointer-events: none;
  font-size: 4rem;
}

.scroller-content {
  animation: the-animation 1s linear forwards;
  animation-timeline: --the-scroller;
}

@keyframes the-animation {
  0% {
    background-color: #ccc;
  }
  100% {
    background-color: #fff;
  }
}

.scroller-content {
  animation: the-animation 1s linear forwards;
  animation-timeline: --the-scroller;
  height: 400%;
  position: relative;
  background-color: aliceblue;
  background-image: linear-gradient(
      to right,
      rgb(0 0 0 / 0.05) 1px,
      transparent 1px
    ),
    linear-gradient(to bottom, rgb(0 0 0 / 0.05) 1px, transparent 1px);
  background-size: 10vh 10vh;
  z-index: -1;
}

:root {
  --scrollbox-border-size: 1em;
  --scrollbox-height: 40vmax;
  --scrollbox-width: calc(var(--scrollbox-height) * 16 / 9);
}
```

`JS`:

```js
const animation = document
  .querySelector(".scroller-content")
  .getAnimations()[0];
const output = document.querySelector(".scroll-progress");
let currentValue = 0;

const updateValue = () => {
  if (animation && animation.currentTime) {
    const newValue = animation.currentTime.value;
    if (newValue != currentValue) {
      output.innerText = `${newValue.toFixed(0)}%`;
      currentValue = newValue;
    }
  }
  requestAnimationFrame(updateValue);
};

requestAnimationFrame(updateValue);
```

- [scroll-driven-animations.style](https://scroll-driven-animations.style/tools/scroll-timeline/progress/)
- [Codepen](https://codepen.io/paraoiawhy/pen/XWyZZmE)

## Scroll-Driven 兼容性

- [CSS property: animation-timeline - caniuse.com](https://caniuse.com/mdn-css_properties_animation-timeline)

## NProgress

- [NProgress - GitHub](https://github.com/rstacruz/nprogress)
- [NProgress - npm](https://www.npmjs.com/package/nprogress)