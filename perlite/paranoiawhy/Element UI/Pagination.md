## 插槽

使用具名插槽 `slot="default"`

```vue
<template slot="default">
</template>
```

并在 `layout` 中指定:

```vue
<el-pagination layout="slot, total, sizes, prev, pager, next"></el-pagination>
```