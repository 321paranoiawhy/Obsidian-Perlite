# document 事件

## visibilitychange

- [Document: visibilitychange event](https://developer.mozilla.org/en-US/docs/Web/API/Document/visibilitychange_event)
- [Document: visibilityState property](https://developer.mozilla.org/en-US/docs/Web/API/Document/visibilityState)

```js
document.addEventListener("visibilitychange", (event) => {});

document.onvisibilitychange = (event) => {};
```

在事件回调内可以使用 `document.visibilityState` 判断当前页面可见度:

```js
if (document.visibilityState === "visible") {
	console.log('visible');
} else if (document.visibilityState === "hidden") {
	console.log('hidden');
}
```

# window 事件

## pageshow

- [Window: pageshow event](https://developer.mozilla.org/en-US/docs/Web/API/Window/pageshow_event)

```js
window.addEventListener("pageshow", (event) => {});

window.onpageshow = (event) => {};
```

## resize

- [Window: resize event](https://developer.mozilla.org/en-US/docs/Web/API/Window/resize_event)

```js
window.addEventListener("resize", (event) => {});

window.onresize = (event) => {};
```

## load

- [Window: load event](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event)

```js
window.addEventListener("load", (event) => {});

window.onload = (event) => {};
```
