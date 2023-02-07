# `Dockerfile`

> [!tip]
> `web/Dockerfile`:
> ```dockerfile
> MAINTAINER sec77 https://github.com/secure-77/Perlite
> ```
> 
> `MAINTAINER` 语法已废弃, 应改为:
> 
> ```dockerfile
> LABEL maintainer="sec77 https://github.com/secure-77/Perlite"
> ```
> [参见这里](https://github.com/apache/couchdb-docker/issues/126)

# 拼写错误

- `perlite/.js/perlite.js` 文件中
	- `// local Graph & Outline Swith` 应为 `// local Graph & Outline Switch`

- `perlite/PerliteParsedown.php` 文件中 `protected function inlineLink($Excerpt)` 上一行 
	- `# handle external Urls` 应为 `# handle external Links`

# 右侧目录点击跳转范围应扩大

> [!warning]
> 仅点击 `a` 标签时才能跳转至相应标题, 实际应当是点击 `div.tree-item-self.is-clickable` 即可跳转相应标题。

源码 `perlite/.js/perlite.js` 中

```js
toc += '<div class="tree-item-self is-clickable"><a href="#' + anchor + '">' + titleText + '</a></div>';
```

改为:

```js
toc += `<a href="#${anchor}"><div class="tree-item-self is-clickable">${titleText}</div></a>`;
```

同时在 `perlite/.styles/perlite.css` 中添加如下 `CSS` 代码:

```css
.tree-item-children a {
  text-decoration: none;
}
```

# 右侧目录渲染问题

> [!warning]
> 当 `h1 ~ h6` 标签内嵌有元素时, 该标题不会出现在右侧的 `Table of Contents` 中。

> [!tip]
> `perlite/.js/perlite.js`:
> ```js
> document.getElementById("mdContent").innerHTML =
> 	document.getElementById("mdContent").innerHTML.replace(
> 		/<h([\d])>([^<]+)<\/h([\d])>/gi,
> ```
> 
> 上述代码中正则表达式应改为:
> 
> ```js
> /<h([\d])>(.*)<\/h([\d])>/gi
> // 或
> // /<h([\d])>([\s\S]*?)<\/h([\d])>/gi
> ```

# 右侧目录可折叠

#TODO

# 添加更多语言高亮

将 `perlite/.js/highlight.min.js` 文件替换为 [hightlight download](https://highlightjs.org/download/) 下载的压缩包中 `hightlight.min.js` 即可。

> [!tip]
> 除 `common` 中列出的语言之外, 可酌情添加语言如:
> - ARM Assembly
> - Dart
> - Dockerfile 
> - Haskell
> - LaTeX
> - ......

# 代码块右上角显示语言

```js
// set content
$("#mdContent").html(result);

const pre = document.querySelectorAll("pre");
pre.forEach((item)=>{
	item.setAttribute("data-lang",item.children[0].classList[0].substr(9));
});
```

# 代码块增加复制按钮

# 代码块左侧展示行号

# 图片居中

> [!warning]
> 默认图片居左对齐。

> [!tip]
> 将 `perlite/.styles/perlite.css` 中 `img` 样式由:
> 
> ```css
> img {
>   display: initial !important;
> }
> ```
> 
> 改为:
> 
> ```css
> img {
>   display: block;
>   margin: 0 auto;
> }
> ```

# 去除图片右上角箭头 

> [!warning]
> 默认图片右上角有一箭头。

> [!tip]
> 将 `perlite/.styles/app.css` 中 `.external-link`类选择器改为 `.external-link:not(img)`

# 内容区域平滑滚动

`perlite/.styles/perlite.css` 中添加如下 `CSS` 代码:

```css
/* 平滑滚动 */
.markdown-rendered {
  scroll-behavior: smooth;
}
```

# 按钮的 `Tooltip`



# TODO

## 代码块折叠功能

## 多彩缩进

`TOC` 部分:

```css
.tree-item-children {
	
}
```

## 多彩文件夹

## 多彩标签

## 标题悬停动效

## 滚动到顶部/底部

## `Tooltip`

各按钮的 `Tooltip` 样式

## 国际化 (部分内容)