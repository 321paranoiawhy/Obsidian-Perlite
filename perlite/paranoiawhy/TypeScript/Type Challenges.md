# First of Array

```ts
type First<T extends any[]> = T extends [] ? never : T[0]
```

`Object` 对象的键只能是 `String` 或 `Symbol`

```ts
T extends string ? 'string' : 'symbol'
```

`PropertyKey` 等价于 `string | number | symbol"`, 表示对象键的类型可以使用 `PropertyKey`:

```ts
T extends PropertyKey
```

`WeakMap` 的键可以是任何合法值

阻止 `a` 标签跳转:

```vue
<a href="javascript:void(0);" @click="e => e.preventDefault ? e.preventDefault() : e.returnValue = false"></a>

<a href="javascript:void(0);" @click="e => return false"></a>
```

阻止默认事件:

```js
// 阻止默认事件
e.preventDefault()
// 阻止事件冒泡
e.stopPropgation()
```

[Append to object](https://typehero.dev/challenge/append-to-object)

```ts
type Util<T> = { [key in keyof T]: T[key] } & {}
// 先表示出 T & Record<U ,V>
type AppendToObject<T, U extends PropertyKey, V> = Util<T & Record<U ,V>>
```

> Error: An index signature parameter type cannot be a literal type or generic type. Consider using a mapped object type instead.

```ts
type T_Union = 'a' | 'b' | 'c'

// Error
type T_Object = {[key: T_Union]: string}

// 改用 mapped types
// OK
type T_Mapped_Object = {[key in T_Union]: string}
// 改用 Record
// OK
type T_Record_Object = Record<T_Union, string>
```

```html
<input type="number"></input>
```

可输入任意数字(可含小数点, 且至多含一位小数点), 特殊情形如下:

- `++1`
- `--1`
- `+-1`
- `-+1`
- `.1`

数字前至多可输入两次符号字符 (`+` / `-`), 至多输入一位小数点

隐藏 `input` 数字输入框右侧按钮:

```css
/* Firefox */
input[type=number] {
	-moz-appearance: textfield;
}

/* Chrome, Safari, Edge, Opera etc */
input[type=number]::-webkit-inner-spin-button, 
input[type=number]::-webkit-outer-spin-button { 
  -webkit-appearance: none;
  margin: 0;
}
```

`Vue2` 组件外使用 `Vuex store`:

```js
// 假定 store 入口文件位于 src/store/index.js
import store from '@/store'

// getters
store.getters.obj
```

`Vue3` 组件外使用 `pinia`:

```ts

```

[Using a store outside of a component - Pinia](https://pinia.vuejs.org/core-concepts/outside-component-usage.html)

`drop_console` 和 `drop_debugger`

```ts
//vite.config.js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

export default defineConfig({
    plugins: [vue()],
    build: {
        minify: 'terser',
        terserOptions: {
            compress: {
                // 生产环境时移除 console 和 debugger
                drop_console: true,
                drop_debugger: true,
            },
        },
    },
})
```

```ts
export default defineConfig(({ mode }) => {
  return {
    esbuild: {
      drop: mode === 'production' ? ['console', 'debugger'] : [],
    }
  }
}
```

```ts
export default defineConfig(({ mode }) => {
  return {
    esbuild: {
      pure: mode === 'production' ? ['console.log'] : [],
    }
  }
}
```

`el-table` 自定义索引列:

```vue
<el-table-column
    label="#" type="index" width="50"
    :index="index => index + 1 + (pagination.page - 1) * pagination.size" />
```

默认的 `index` 方法为 `index => index + 1`

# 静态资源处理

- [Assets - Nuxt3](https://nuxt.com/docs/getting-started/assets)
- [Images - Nuxt2](https://v2.nuxt.com/docs/directory-structure/assets/#images)
- [new URL - Vite](https://vitejs.dev/guide/assets.html#new-url-url-import-meta-url)

```vue
<template>
  <img src="/img/nuxt.png" alt="Discover Nuxt 3" />
</template>
```

```vue
<template>
  <img src="~/assets/img/nuxt.png" alt="Discover Nuxt 3" />
</template>
```

使用 `require`:

```vue
<img :src="require('./img/logo.svg')">
```

使用 `new URL`:

```vue
<script setup lang="ts">
const imgHref = new URL('/assets/svgo/logo.svg', import.meta.url).href
</script>
<template>
  <img :src="imgHref">
</template>
```

Does not work with SSR

This pattern does not work if you are using Vite for Server-Side Rendering, because `import.meta.url` have different semantics in browsers vs. Node.js. The server bundle also cannot determine the client host URL ahead of time.

- [vite-plugin-require](https://www.npmjs.com/package/vite-plugin-require)

# 性能优化

- `preload`
- `preconnect`
- `prefetch`
- `lazy load`
- [前端优秀实践不完全指南](https://juejin.cn/post/6932647134944886797)

# 链表

- [Doubly Linked-List in TypeScript](https://www.devmaking.com/learn/data-structures/doubly-linked-list/typescript/)

# 响应式 localStorage

- [StorageEvent - MDN](https://developer.mozilla.org/en-US/docs/Web/API/StorageEvent)

```js
const onStorageUpdate = (event) => {
	console.log(event.key, event.newValue, event.oldValue, event.storageArea, event.utl)
}

window.addEventListener("storage", onStorageUpdate)
```

- [Reactive Local Storage](https://github.com/icyJoseph/use-reactive-local-storage)
- [useStorage - VueUse](https://vueuse.org/core/useStorage/#usestorage)
- [Unstorage](https://unstorage.unjs.io/)
- [lru-cache - npm](https://www.npmjs.com/package/lru-cache)
- [localForage - GitHub](https://github.com/localForage/localForage)

# eslint

当前项目内安装:

```bash
# 安装
npm install eslint --save-dev

# 初始化 eslint 配置
./node_modules/.bin/eslint --init
# 等价于
npm init @eslint/config
```

全局安装:

```bash
pnpm install eslint i -g

eslint --init
```

配置文件可选格式:

- `JavaScript` -> `.eslintrc.js`
- `JavaScript(ESM)` -> `.eslintrc.cjs`
- `YAML` -> `.eslintrc.yaml` 或 `.eslintrc.yml`
- `JSON` -> `.eslintrc.json`
- `package.json` -> 配置 `eslintConfig` 属性

配置文件优先级(由高到低):

1. `.eslintrc.js`
2. `.eslintrc.cjs`
3. `eslintrc.yaml`
4. `.eslintrc.yml`
5. `.eslintrc.json`
6. `package.json`

配置规则说明:

- `off` <-> `0`, 关闭
- `warn` <-> `1`, 警告
- `error` <-> `2`, 错误

属性说明:

- `env` 指定代码运行的宿主环境, 如 `browser`、`node`、`es6`、`es2021`
- `extends` 指定应用的 `eslint` 规范, 如 `standard`、`standard-with-typescript`、`plugin:vue/vue3-essential`
- `globals` 声明在代码中的自定义全局变量, 如 `global`、`$global`
- `parserOptions` 设置解析器选项
- `plugins` 引用的第三方插件
- `rules` 启用额外规则或覆盖默认规则

测试文件:

```bash
eslint example.js
```

对项目代码执行 `eslint` 检查:

```bash
npm run lint
```

配置 `husky` 和 `lint-staged`:

```bash
pnpm i husky lint-staged -D
```

# 限制最大并发请求数

- [axios 请求并发数 axios 并发数限制](https://blog.51cto.com/u_16099188/7194117)

- `Promise.all`
- `Axios` 的 `axios.all`

`Vue` 切换路由时取消之前的所有未完成请求:

```js
router.beforeEach((to, from, next) => {
    pendingXHRMap.forEach((cancel) => {
        cancel();
    });
    pendingXHRMap.clear()
})
```

- [来，一起偷偷优化前端请求性能，然后惊艳所有人
](https://zhuanlan.zhihu.com/p/366137430)


# 文本两端对齐

多行文本:

```css
.justify {
	text-align: justify;
}
```

多行文本最后一行如果宽度不够则不会两端对齐而是居左对齐

单行文本:

```css
.justify {
	text-align: justify;
	text-align-last: justify;
}
```

`shadow` 语法:

```css
box-shadow: <offset-x> <offset-y> <blur-radius> <spread-radius>;
```