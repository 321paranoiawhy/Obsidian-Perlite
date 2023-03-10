# 禁用缓存

## `HTML`

`index.html` :

```html
<meta http-equiv="Pragma" content="no-cache">
<meta http-equiv="Cache-Control" content="no-cache">
<meta http-equiv="Expires" content="0">
```

> [!danger]
> 上述方案存在兼容性问题,  `Chrome` 浏览器中不生效。

## 浏览器控制台中禁用 `GET` 请求缓存

1. `Network` 标签页勾选 `Disable cache` (**while DevTools is open**)
2. `Network` 标签页选择请求资源, 右键选择 `Clear broswer cache`

## 快捷键清除缓存

`ctrl + shift + delete` 或 `ctrl + F5` 手动清除当前网页缓存。

## 文件名中加入 `Hash` 、`UUID` `tag` 或随机数

文件名加入 `Hash` :

- [打包的 3 种 hash 值你知道吗? 当年我校招时被这题难倒了!](https://juejin.cn/post/7060688758370205733)
- [output.filename - webpack](https://webpack.js.org/configuration/output/#outputfilename)
- [Output Filenames - webpack](https://webpack.js.org/guides/caching/#output-filenames)
- [What is the purpose of webpack [hash] and [chunkhash]?](https://stackoverflow.com/questions/35176489/what-is-the-purpose-of-webpack-hash-and-chunkhash)
- [理解 webpack 的 hash ，contenthash，chunkhash](https://xinyuehtx.github.io/post/%E7%90%86%E8%A7%A3webpack%E4%B8%8D%E5%90%8Chash%E5%80%BC%E7%9A%84%E4%BD%9C%E7%94%A8.html)

文件名加入 `UUID` :

```js
const script = document.createElement("script");
script.src = `test.${crypto.randomUUID()}.js`;
```

文件名加入 `tag` :

```js
const script = document.createElement("script");
script.src = `test.js?tag=123456`;
```

文件名加入随机数:

```js
const script = document.createElement("script");
script.src = `test.${Math.random()}.js`;
// script.src = `test.js?random=${Math.random()}`;
```

## 文件名中加入 `version`

```js
const script = document.createElement("script");
script.src = `test.js?version=1.0`;
```

> [!tip]
> 关于 `CVS (Concurrent Versions System)` :
> 
> - [CVS—Concurrent Versions System](https://www.gnu.org/software/trans-coord/manual/cvs/cvs.html)
> - [Concurrent Versions System - Wikipedia](https://en.wikipedia.org/wiki/Concurrent_Versions_System)

## 后端处理

`Response Headers` 设置 `cache-control` 为 `no-cache` 。