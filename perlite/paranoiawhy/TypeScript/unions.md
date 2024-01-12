# union types

```typescript
type bool = true | false;
```

# typeof

```javascript
// string / number / boolean / undefined / function
typeof s === "string";
typeof n === "number";
typeof b === "boolean";
typeof undefined === "undefined";
typeof f === "function";

// array
Array.isArray(a);
```

获取数组值所构成的联合类型:

```ts
// as const 必不可少
const typeArr = ['text', 'image', 'video', 'audio'] as const

// type: 'text' | 'image' | 'video' | 'audio'
type AllType = typeof typeArr[number]
```

# `Element-Plus Icons`

- [element-plus Icon](https://element-plus.org/en-US/component/icon.html)
- [element-plus - Nuxt Modules](https://nuxt.com/modules/element-plus)

## 非 `Nuxt` 项目

```vue
<script>
import { ArrowRight } from '@element-plus/icons-vue'
</script>

<template>
<el-icon><ArrowRight /></el-icon>
</template>
```

## `Nxut` 项目

局部按需引入:

```vue
<script>
import { ArrowRight } from '@element-plus/icons-vue'
</script>

<template>
<el-icon><ArrowRight /></el-icon>
</template>
```

`Nuxt` 中作为 `Plugin` 全局引入:

```ts
import * as ElementPlusIconsVue from '@element-plus/icons-vue'

export default defineNuxtPlugin(async (NuxtApp) => {
  // NuxtApp: https://nuxt.com/docs/guide/going-further/internals

  // 全局组件引入
  for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
    NuxtApp.vueApp.component(key, component)
  }
})
```

或直接按如下方式使用:

```vue
<template>
<ElIconArrowRight/>
</template>
```

# UnoCSS

后缀 `!` 表示 `!important`

`width: 100% !important;` -> `w-full!`

前缀:
- `hover-`

## `shortcuts`

## 常用原子类

- `w-100%`、`w-full` -> `width: 100%;`
- `h-100%`、`h-full` -> `height: 100%;`
- `position-absolute` -> `position: absolute;`

### 圆角相关

- `rounded-1/2` -> `border-radius: 50%;`
- `rounded-1` -> `border-radius: 1px;`

## 文字相关

`line-height`:

- `lh-1` -> `line-height: 1px;`

`flex`:

- `flex` -> `display: flex;`
- `flex-1` -> `flex: 1;`
- `items-center` -> `align-items: center;`
- `flex-row` -> `flex-direction: row`
- `flex-col` -> `flex-direction: column`
- `flex-shrink-0` -> `flex-shrink: 0;`
- `gap-x-16` -> `column-gap: 16px;`
- `gap-y-16` -> `row-gap: 16px;`

- `overflow-hidden` -> `overflow: hidden;`

`font-[number]` 表示 `font-weight: number;`, 如 `font-100` ~ `font-900`

- `font-extralight` -> `font-weight: 200;`
- `font-light` -> `font-weight: 300;`
- `font-normal` -> `font-weight: 400;`
- `font-medium` -> `font-weight: 500;`
- `font-semibold` -> `font-weight: 600;`
- `font-extrabold` -> `font-weight: 800;`
- `font-bold` -> `font-weight: bold;`
- `font-extrabold` -> `font-weight: 800;`
- `font-black` -> `font-weight: 900;`, alias: `fw-black`, `fw-900`, `font-900`

- `cursor-pointer` -> `cursor: pointer;`
- `self-start` -> `align-self: start;`
- `object-contain` -> `object-fit: contain;`
- `object-cover` -> `object-fit: cover;`
- `block` -> `display: block;`

`truncate`:

```css
.truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```

限制只能输入正整数:

```vue
<!-- 正则表达式 /[^\d]/g 等价于 /\D/g -->
<el-input v-model="inputModel" @input="v => inputModel = v.replace(/\D/g, '')"></el-input>
```