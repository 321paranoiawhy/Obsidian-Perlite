# `CSS`

[div.proposed-sets-list__container-scroll](https://unicode-table.com/cn/blocks/arrows/)
[::-webkit-scrollbar - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/::-webkit-scrollbar)
[Custom Scrollbars in WebKit - CSS Tricks](https://css-tricks.com/custom-scrollbars-in-webkit/)
[How TO - Custom Scrollbar - W3Schools](https://www.w3schools.com/howto/howto_css_custom_scrollbar.asp)
[Customize the Browser's Scrollbar with CSS](https://codepen.io/akinjide/pen/BpggrZ)

```CSS
.scrollbar {
	--scrollbar-width: 4px; /* 竖直滚动条宽度  */
	--scrollbar-height: 4px; /* 水平滚动条高度 */
	--scrollbar-background-color: #f9f9fd;
	
	--scrollbar-thumb-border-radius: 4px;
	--scrollbar-thumb-background-color: #b8bdc1;
	
	--scrollbar-track-border-radius: 10px;
	--scrollbar-track-background-color: #f9f9fd;
}

.scrollbar::-webkit-scrollbar {
	width: var(--scrollbar-width);
	height: var(--scrollbar-height);
	background-color: var(--scrollbar-background-color);
}

/* 滚动条上的滚动滑块 */
.scrollbar::-webkit-scrollbar-thumb {
	border-radius: var(--scrollbar-thumb-border-radius);
	background-color: var(--scrollbar-thumb-background-color);
}

/* 滚动条轨道 */
.scrollbar::-webkit-scrollbar-track {
	box-shadow: inset 0 0 6px rgb(0 0 0 / 20%);
	border-radius: var(--scrollbar-track-border-radius);
	background-color: var(--scrollbar-track-background-color);
}
```

`Codepen`: [](https://codepen.io/paraoiawhy/pen/JjZzgKw)

# `Div` + `JavaScript`

```HTML

```

```JavaScript
```

# `Obsidian` 滚动条

```css
.theme-light {
	--mono-rgb-0: 255, 255, 255;
    --mono-rgb-100: 0, 0, 0;
}

body {
	--radius-s: 4px;
    --radius-m: 8px;
    --radius-l: 10px;
    --radius-xl: 16px;
    
    --scrollbar-active-thumb-bg: rgba(var(--mono-rgb-100), 0.2);
    --scrollbar-bg: rgba(var(--mono-rgb-100), 0.05);
    --scrollbar-thumb-bg: rgba(var(--mono-rgb-100), 0.1);
}

body:not(.native-scrollbars) ::-webkit-scrollbar {
    width: 12px;
    height: 12px;
    border-radius: var(--radius-l);
    background-color: transparent;
}

body:not(.native-scrollbars) ::-webkit-scrollbar-corner {
    background: transparent;
}

body:not(.native-scrollbars) ::-webkit-scrollbar-thumb {
    background-color: var(--scrollbar-thumb-bg);
    border-radius: var(--radius-l);
    background-clip: padding-box;
    border-style: solid;
    border-color: transparent;
    border-image: initial;
    border-width: 3px 3px 3px 2px;
    min-height: 45px;
}

body:not(.native-scrollbars) ::-webkit-scrollbar-track {
    background-color: transparent;
}
```