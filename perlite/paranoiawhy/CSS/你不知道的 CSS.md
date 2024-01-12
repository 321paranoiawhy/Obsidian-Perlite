# column-count

对 `p` 标签分栏(两栏):

```css
p {
	column-count: 2;
}
```

# text-overflow

单行文本超出显示 `...`:

```css
.text-overflow {
  white-space: nowrap; 
  width: 200px; 
  overflow: hidden;
  text-overflow: ellipsis;
}
```

多行文本超出显示 `...`:

```css
```

# 输入框左右震动动画

```css
input:invalid{
      animation: shake 0.2s ease-in-out 0s 2;
      box-shadow: 0 0 0.4em red;
}
  @keyframes shake {
      0% { margin-left: 0rem; }
      25% { margin-left: 0.5rem; }
      75% { margin-left: -0.5rem; }
      100% { margin-left: 0rem; }
}
```

# 选择器

第一个元素:

```css
:first-child
```

最后一个元素:

```css
:last-child
```

最后两个元素:

```css
:nth-last-child(-n + 2)
```

- [Dynamic Components - Nuxt](https://nuxt.com/docs/guide/directory-structure/components#dynamic-components)

```vue
const searchIcon = resolveComponent('ElIconSearch')

<ElInput  
  v-model="personNameKeyword"  
  class="mt-30 h-54"  
  placeholder="搜索人名关键字" :suffix-icon="searchIcon as any" />
  
<ElInput  
  v-model="personNameKeyword"  
  class="mt-30 h-54"  
  placeholder="搜索人名关键字">  
  <template #suffix>  
    <ElIconSearch />  
  </template>  
</ElInput>
```

`vue3` 动态绑定 `ref`:

```vue
<script setup lang="ts">
type T_SectionUnion = 'section1' | 'section2' | 'section3' | 'section4' | 'section5'

const sectionRefs = reactive<{ [key in T_SectionUnion]: HTMLElement | null }>({  
  section1: null,  
  section2: null,  
  section3: null,  
  section4: null,  
  section5: null,  
})
</script>

<template>
	<div :ref="el => el && (sectionRefs.section1 = el)"></div>
</template>
```

上述方式为使用 `ref` 的回调函数, 也可以利用 `getCurrentInstance`:

```vue
<script setup lang="ts">
import { getCurrentInstance, onMounted, ref } from "vue"

const { proxy } = getCurrentInstance()

onMounted(() => {
	console.log(proxy.$refs.exampleRef)
	console.log(proxy.$refs['exampleRef'])
})
</script>
```