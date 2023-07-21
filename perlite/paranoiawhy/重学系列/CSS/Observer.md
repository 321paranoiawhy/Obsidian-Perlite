## MutationObserver

- [MutationObserver - MDN](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver)
- [Interface MutationObserver](https://dom.spec.whatwg.org/#interface-mutationobserver)

## IntersectionObserver

- [IntersectionObserver - MDN](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver)
- [The IntersectionObserver interface - W3C](https://w3c.github.io/IntersectionObserver/#intersection-observer-interface)

## ResizeObserver

`ResizeObserver` 相比于监听 `window` 的 `resize` 事件, 更精准且高效, 性能上也更优。

> [!tip]
> 仅 `window` 支持 `resize` 事件。

- [ResizeObserver - MDN](https://developer.mozilla.org/en-US/docs/Web/API/ResizeObserver)
- [ResizeObserver interface](https://drafts.csswg.org/resize-observer/#resize-observer-interface)

检测浏览器是否支持 `ResizeObserver`:

```js
if('ResizeObserver' in window){
	// 浏览器支持 ResizeObserver
}
```

`ResizeObserver` **Polyfill**:

- [Resize Observer Polyfill - GitHub](https://github.com/juggle/resize-observer)
- [Resize Observer Polyfill Playground](https://juggle.studio/resize-observer/)
- [@juggle/resize-observer - npm](https://www.npmjs.com/package/@juggle/resize-observer)

`ResizeObserver` **Polyfill** 使用:

```js
import { ResizeObserver as Polyfill } from '@juggle/resize-observer';

// 如果浏览器自身支持, 则使用浏览器自带的 window.ResizeObserver
// 否则, 使用 ResizeObserver Polyfill
const ResizeObserver = window.ResizeObserver || Polyfill;
```

## PerformanceObserver

- [PerformanceObserver - MDN](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver)
- [The PerformanceObserver interface](https://w3c.github.io/performance-timeline/#dom-performanceobserver)