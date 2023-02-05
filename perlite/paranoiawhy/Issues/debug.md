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

# `TOC`

当 `h1 ~ h6` 标签内嵌有元素时, 该标题不会出现在右侧的 `Table of Contents` 中。

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

# 图片居中

> [!tip]
> 将 `perlite/.styles/perlite.css` 中 `img` 样式由:
> 
> ```css
> img {
>   display: initial !important;
>   margin: 0 auto;
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

> [!tip]
> 将 `perlite/.styles/app.css` 中 `.external-link`类选择器改为 `.external-link:not(img)`

# TODO

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