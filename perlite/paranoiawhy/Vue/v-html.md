# `v-html` 不执行 `script` 标签

- [为什么 vue v-html 不执行 script 代码？](https://mp.weixin.qq.com/s?__biz=Mzg5Mjc2NDYwMg==&mid=2247483940&idx=1&sn=84ec44582650c2352b4649652a0f591a&chksm=c0386af1f74fe3e74f56ee74f9adafaf61d5a7061f9ca3d146ccc916746636bd5af245b654be&token=114373383&lang=zh_CN#rd)

```vue
<template>
	<div v-html="divHTML"></div>
</template>

<script setup lang="ts">
const divHTML = "<span>test</span><script>console.log(123456789);</script>";
</script>
```

[Twitter link](https://twitter.com/johnvoorhees/status/1437735225086316548?s=21)

[Twitter link](https://twitter.com/johnvoorhees/status/1437735225086316548?s=21)

```gist
5149b8848cb05f20efbc21fa750d7d2e
```