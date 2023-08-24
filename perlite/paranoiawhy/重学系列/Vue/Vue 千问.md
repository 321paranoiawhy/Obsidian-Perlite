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
