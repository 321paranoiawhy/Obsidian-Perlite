- [aspect-ratio - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio)
- [aspect-ratio - Browser Compatibility](https://www.lambdatest.com/web-technologies/aspect-ratio)
- [CSS property: aspect-ratio - caniuse](https://caniuse.com/mdn-css_properties_aspect-ratio)
- [CSS Feature Queries - caniuse](https://caniuse.com/css-featurequeries)

```css
div {
	aspect-ratio: 16 / 9;
}

img {
	aspect-ratio: 4 / 3;
}
```

`aspect-ratio` 支持以下关键字语法:

- `unset`
- `initial`
- `inherit`
- `auto`

如浏览器不支持该特性, 可使用 `padding-top` 方式做兼容处理, 这被称为 `Padding Top Hack`

```css
@supports not (aspect-ratio: 16 / 9) {
	.container {
		position: relative;
		padding-top: calc(9 / 16 * 100%);
		overflow: hidden;
	}

	.container img {
		position: absolute;
		top: 0;
		bottom: 0;
		left: 0;
		right: 0;
		object-fit: cover;
	}
}
```

注意, 原本需固定宽高比的元素外层需包裹一层 `div`, 相比之下, `aspect-ratio` 方案则无此需求。

使用 `JS` 检测浏览器是否支持 `aspect-ratio` 特性:

```js

```