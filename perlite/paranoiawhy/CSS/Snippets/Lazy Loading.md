# 懒加载库

- [lazysizes](https://github.com/aFarkas/lazysizes)
- [lazysizes demo](http://afarkas.github.io/lazysizes/#examples)
- [vanilla lazyload](https://github.com/verlok/vanilla-lazyload)
- [lozad.js](https://github.com/ApoorvSaxena/lozad.js)
- [react-lazyload](https://github.com/twobin/react-lazyload)
- [yall.js](https://github.com/malchata/yall.js)

# image

```html
<img src="https://unsplash.dogedoge.com/photos/UAGqBTkMeA4" loading="lazy" />
<iframe src="https://www.google.com/" loading="lazy"></iframe>
```

> [!tip] `loading` 属性枚举值
> - `lazy` : 懒加载
> - `eager` : 立即加载
> - `auto` : 交由浏览器自行决定

## 检测浏览器是否支持 loading 属性

以下三种方式皆可检测浏览器是否支持 `loading` 属性:

```js
const isLoadingSupported = "loading" in HTMLImageElement.prototype;
// const isLoadingSupported = "loading" in document.createElement("img");
// const isLoadingSupported = "loading" in new Iamge();
```

对于 `iframe` 标签:

```js
const isLoadingSupported = "loading" in HTMLIFrameElement.prototype;
// const isLoadingSupported = "loading" in document.createElement("iframe");
```

> [!caution]
> - [FireFox](https://caniuse.com/loading-lazy-attr) 不支持 `iframe` 标签的 `loading` 属性。
> - [iframe browser compatibility - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe#browser_compatibility)

## 一些支持 loading 属性的 HTML 标签

- `img`
- `iframe`

## 检测图片加载完成

使用 `image` 元素的 [compelete 属性](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/complete):

```js
const image = document.querySelector("img");
const imageLoadingDone = image.complete;
```

```js
Object.getOwnPropertyDescriptor(document.querySelector("img").__proto__, "complete");
```

`img` 加载完成的回调事件 `onload` :

```js
const image = document.querySelector("img");
image.onload = () => {};
```

## 计算图片加载耗时

```js
const loadImage = (url) =>
  new Promise((resolve, reject) => {
    let image = new Image();
    image.onload = () => {
      resolve(url);
      console.timeEnd("图片加载耗时: ");
      image = undefined;
    };
    image.onerror = () => reject(url);
    image.src = url;
  });

console.time("图片加载耗时: ");

loadImage("https://images.pexels.com/photos/1684880/pexels-photo-1684880.jpeg");
```

## 检测图片是否有缓存

```js
const image = document.querySelector("img");
const imageHasCache = image.naturalWidth || image.naturalHeight;
```

## 图片链接失效

使用 `image` 元素的 `onerror` 事件:

```js
const image = document.querySelector("img");
image.onerror = () => {};
```

- [图片加载失败后CSS样式处理最佳实践](https://www.zhangxinxu.com/wordpress/2020/10/css-style-image-load-fail/)

## Reference

- [Use lazy loading to improve loading speed](https://web.dev/lazy-loading/)
- [Browser-level image lazy loading for the web](https://web.dev/browser-level-image-lazy-loading/)
- [Lazy loading - MDN](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading)
- [Lazy Loading Images – The Complete Guide](https://imagekit.io/blog/lazy-loading-images-complete-guide/)
- [Native image lazy-loading for the web!](https://addyosmani.com/blog/lazy-loading/)
- [It's time to lazy-load offscreen iframes!](https://web.dev/iframe-lazy-loading/#can-i-lazy-load-iframes-cross-browser-yes)
- [Lazy-load images and video](https://web.dev/fast/#lazy-load-images-and-video)
- [Lazy loading images](https://web.dev/lazy-loading-images/)
- [Lazy loading video](https://web.dev/lazy-loading-video/)

# video

设置 `video` 的 `preload` 属性为 `none` :

```html
<!-- disable preloading -->
<video controls preload="none" width="300">
  <source
    src="https://file-examples.com/storage/fe0b804ac5640668798b8d0/2017/04/file_example_MP4_480_1_5MG.mp4"
    type="video/mp4"
  />
</video>
```

> [!caution]
> 须确保未设置 `autoplay` 属性, 否则 `preload` 属性无效。

设置 `video` 的 `poster` 属性占位, 避免浏览器间样式差异:

```html
<video controls preload="none" poster="img/cover.jpg" width="300">
  <source src="https://file-examples.com/storage/fe0b804ac5640668798b8d0/2017/04/file_example_MP4_480_1_5MG.mp4" type="video/mp4" />
</video>
```

## Reference

- [https://usefulangle.com/post/287/html-video-lazy-load](https://usefulangle.com/post/287/html-video-lazy-load)

# iframe

## 嵌入工具

- [Lite YouTube Embed](https://github.com/paulirish/lite-youtube-embed)

## 检测 iframe 加载完成

```js
const iframe = document.createElement("iframe");
iframe.src = "http://sc.jb51.net";

// IE
if (iframe.attachEvent) {
  iframe.attachEvent("onload", () => {
    console.log("Local iframe is now loaded.");
  });
  // not IE
} else {
  iframe.onload = () => {
    console.log("Local iframe is now loaded.");
  };
}
```

## 通信

使用 `postMessage` :

```js
// iframe
const iframe = document.querySelector("iframe");
iframe.contentWindow.postMessage("message from iframe", "*");
```

```js
// 父页面
window.addEventListener(
  "message",
  (e) => {
    console.log(e.data, "接收的数据");
  },
  false
);
```
