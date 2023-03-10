# 单个折叠

## max-height

`HTML` :

```html
<div class="container">
  <div class="heading">Heading</div>
  <div class="content">
    Lorem ipsum dolor, sit amet consectetur adipisicing elit. Laborum natus
    ipsum enim reprehenderit labore, necessitatibus eligendi itaque excepturi
    iure praesentium quia. Modi facere veritatis beatae libero, necessitatibus
    totam nulla. Numquam, culpa perspiciatis. Perspiciatis illo nesciunt
    maiores, fugiat sit illum? Ab, asperiores beatae at nihil totam praesentium
    fuga! Esse impedit totam id expedita dicta quae inventore illum pariatur
    doloribus quibusdam accusantium ut assumenda quia facilis sequi corporis,
    amet delectus? Officiis corrupti ducimus quam repellat facilis itaque
    similique quaerat assumenda blanditiis, qui porro nobis ratione impedit
    exercitationem repellendus temporibus id? Tempora libero maiores magni
    reiciendis qui odio aliquid ipsum sequi atque autem.
  </div>
</div>
```

### hover

- [How can I transition height: 0; to height: auto; using CSS?](https://stackoverflow.com/questions/3508605/how-can-i-transition-height-0-to-height-auto-using-css)

```css
.content {
	max-height: 0;
	overflow: hidden;
	transition: max-height 0.3s ease-in-out;
}

.container:hover .content {
	max-height: 300px;
}
```

> [!tip]
> - `transition` 属性里不能是 `height` 而应为 `max-height`
> - 未 `hover` 时, `content` 最大高度为 `0` 且溢出隐藏
> - `hover` 时, `content` 设定最大高度为某一确定值, 而不能随内容自动扩展

- [Codepen Demo](https://codepen.io/paraoiawhy/pen/BaOmpvz)

### click

```css
.container .content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s ease-in-out;
}

.container .open {
  max-height: 500px;
}
```

```js
const container = document.querySelector(".container");
const content = container.querySelector(".content");
container.onclick = () => {
  content.classList.toggle("open");
};
```

> [!tip]
> - 利用有 `is-collapsed` 类名和无 `is-collapsed` 类名的样式差异
> - `JS` 控制类名的有无: `element.classList.toggle(className)`
> - [jQuery](http://api.jquery.com/toggle/) 控制类名的有无: `element.toggle(className)`

- [Codepen Demo](https://codepen.io/paraoiawhy/pen/QWVOdpE)

## grid

`HTML` :

```html
<div class="container">
  <div class="heading">Heading</div>
  <div class="grid">
    <div class="grid-inner">
      <div class="content">
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Laborum natus
        ipsum enim reprehenderit labore, necessitatibus eligendi itaque excepturi
        iure praesentium quia. Modi facere veritatis beatae libero, necessitatibus
        totam nulla. Numquam, culpa perspiciatis. Perspiciatis illo nesciunt
        maiores, fugiat sit illum? Ab, asperiores beatae at nihil totam praesentium
        fuga! Esse impedit totam id expedita dicta quae inventore illum pariatur
        doloribus quibusdam accusantium ut assumenda quia facilis sequi corporis,
        amet delectus? Officiis corrupti ducimus quam repellat facilis itaque
        similique quaerat assumenda blanditiis, qui porro nobis ratione impedit
        exercitationem repellendus temporibus id? Tempora libero maiores magni
        reiciendis qui odio aliquid ipsum sequi atque autem.
      </div>
    </div>
  </div>
</div>
```

### hover

```css
.grid {
  display: grid;
  grid-template-rows: 0fr;
  transition: grid-template-rows 0.3s ease-in-out;
}

.container:hover .grid {
  grid-template-rows: 1fr;
}

.grid-inner {
  overflow: hidden;
}
```

[Codepen Demo](https://codepen.io/paraoiawhy/pen/VwGrRxg)

### click

```css
.grid {
  display: grid;
  grid-template-rows: 0fr;
  transition: grid-template-rows 0.3s ease-in-out;
}

.grid.open {
  grid-template-rows: 1fr;
}

.grid-inner {
  overflow: hidden;
}
```

```js
const container = document.querySelector(".container");
const grid = document.querySelector(".grid");

container.onclick = () => {
  grid.classList.toggle("open");
};
```

> [!tip]
> - 可实现 `content` 高度从 `0` 到 `auto` 的过渡效果
> - [grid 兼容性](https://caniuse.com/css-grid)
> - [grid-template-rows 兼容性](https://caniuse.com/mdn-css_properties_grid-template-rows)

[Codepen Demo](https://codepen.io/paraoiawhy/pen/mdGqoWo)
[Grid 网格轨道 transition](https://codepen.io/brandonzhang/pen/NWBZrMr)

# transform-origin: top

利用 `transform-origin: top`、`transform: scaleY(0)` 和 `transform: scaleY(1)` :

```html
<div class="container">
  <div class="heading">Heading</div>
  <div class="content">
    Lorem ipsum dolor, sit amet consectetur adipisicing elit. Laborum natus
    ipsum enim reprehenderit labore, necessitatibus eligendi itaque excepturi
    iure praesentium quia. Modi facere veritatis beatae libero, necessitatibus
    totam nulla. Numquam, culpa perspiciatis. Perspiciatis illo nesciunt
    maiores, fugiat sit illum? Ab, asperiores beatae at nihil totam praesentium
    fuga! Esse impedit totam id expedita dicta quae inventore illum pariatur
    doloribus quibusdam accusantium ut assumenda quia facilis sequi corporis,
    amet delectus? Officiis corrupti ducimus quam repellat facilis itaque
    similique quaerat assumenda blanditiis, qui porro nobis ratione impedit
    exercitationem repellendus temporibus id? Tempora libero maiores magni
    reiciendis qui odio aliquid ipsum sequi atque autem.
  </div>
</div>
```

### hover

```css
.content {
  transform-origin: top;
  transform: scaleY(0);
  transition: all 0.3s ease-in-out;
}

.container:hover .content {
  transform: scaleY(1);
}
```

> [!tip]
> - 这里 `content` 的 `transform-origin` 属性值须为 `top` , 可根据实际需要更改其值, 如 `bottom` 等
> - `scaleY` 也可改为 `scaleX` , 为横向展开折叠效果
> - `transition` 中的 `all` 可进一步明确为 `transform`
> - 上述方式可实现 `content` 高度由 `0` 到 `auto` 的过渡效果

[Codepen Demo](https://codepen.io/paraoiawhy/pen/QWVOoVG)

### click

```css
.content {
  transform-origin: top;
  transform: scaleY(0);
  transition: transform 0.3s ease-in-out;
}

.open {
  transform: scaleY(1);
}
```

```js
const container = document.querySelector(".container");
const content = container.querySelector(".content");
container.onclick = () => {
  content.classList.toggle("open");
};
```

[Codepen Demo](https://codepen.io/paraoiawhy/pen/dyqZrwr)

# 手风琴 Accordion

手风琴指多个 `collapse` 组件, 但最多只能有一个处于展开状态, 可参考 [Collapse Accordion - Element plus](https://element-plus.org/en-US/component/collapse.html#accordion)。

# 图标样式和动画

## > 和 

## 和 ^