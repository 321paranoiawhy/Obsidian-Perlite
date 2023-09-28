# 避免 null 上取属性

第一种方式, 使用 `&&`:

```vue
<div>{{ item.info && item.info.content }}</div>
```

第二种方式, 使用 `v-if`:

```vue
<div v-if="item.info">{{ item.info.content }}</div>
```

第三种方式, 使用 `?.`:

```vue
<div>{{ item.info?.content }}</div>

<div>{{ item?.info?.content }}</div>
```

## 如何最快调试 `web` 网页

给所有元素加上红色边框:

```css
* {
	border 1px solid red;
}
```

# 环境变量类型提示

`env.d.ts`:

```ts
/// <reference types="vite/client" />

interface ImportMetaEnv {
  readonly VITE_APP_BASE_URL: string
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

```vue
<script>
console.log(import.meta.VITE_APP_BASE_URL);
</script>
```

# Vite

Vite 仅执行 `.ts` 文件的转译工作，**并不执行** 任何类型检查。并假定类型检查已经被你的 `IDE` 或构建过程处理了。
