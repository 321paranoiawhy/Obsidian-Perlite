# Vue 3

## 挂载全局属性、方法和组件

根目录下的 `main.js` 或 `main.ts`:

```ts
import { createApp } from 'vue'
import App from './App.vue'
const app = createApp(App)

import GlobalComponent from '@/components/GlobalComponent.vue'

// 挂载全局属性
app.config.globalProperties.$globalName = 'I am a global name.'

//挂载全局方法
app.config.globalProperties.$globalMethod = () => {
	console.log('I am a global anonymous function')
}

// 挂载全局组件
// https://vuejs.org/guide/components/registration.html#global-registration
app.component('GlobalComponent', GlobalComponent)

app.mount('#app')
```

获取全局属性和方法:

`example.vue`

```ts
<script setup lang='ts'>
import { getCurrentInstance } from "vue";

const { proxy } = getCurrentInstance();

// 获取全局属性
console.log(proxy.$globalName); // 'I am a global name.'
// 获取全局方法
proxy.$globalMethod(); // 'I am a global anonymous function'

</script>
```
