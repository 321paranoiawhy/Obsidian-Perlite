# `Dockerfile`

> [!tip]
> `web/Dockerfile`:
> ```dockerfile
> MAINTAINER sec77 https://github.com/secure-77/Perlite
> ```
> 
> `MAINTAINER` 语法已废弃, 应改为:
> 
> ```dcockerfile
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

# 多彩标签

# 多彩文件夹

# 多彩缩进

```css
.tree-item-children {
	
}
```