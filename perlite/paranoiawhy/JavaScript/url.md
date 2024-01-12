# hash

```js
// 获取 url 上的哈希值, 包含 # 符号
// /example/#test -> #test
window.location.hash
```

如果不支持 `window.location.hash`, 可以先尝试找到最后一个 `#` 符号:

```js
const lastHashIndex = window.location.lastIndex('#')

if (~lastHashIndex) {
	const hash = window.location.slice(lastHashIndex)
}
```