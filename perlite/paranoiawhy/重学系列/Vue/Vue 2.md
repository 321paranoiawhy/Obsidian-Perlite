## this.$emit('update:props')

父组件:

```vue
<child :show.sync="show"><child>
```

子组件:

```vue
<template>
	<div v-if="show"></div>
	<div @click="onClick"></div>
</template>

<script>
export default {
    props: {
        show: {
            type: Boolean,
            required: true,
        },
    },
    methods: {
	    onClick() {
		    this.$emit('update:show', false);
	    },
    },
}
</script>
```

## vuex 使用

安装:

```bash
npm install vuex@3 --save
```

`src/store/index.js`:

```js
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);

// 创建一个新的 store 实例
const store = new Vuex.Store({
  strict: process.env.NODE_ENV != "production",
  state: {
    count: 0,
  },
  mutations: {
    add(state, payload) {
	    state.count++;
    },
    minus(state, payload) {
	    state.count--;
    },
});
export default store;
```

`main.js`:

```js
import store from './store/index.js';

new Vue({
	el: '#app',
	// router
	router: router,
	// store,
	store: store,
	render: h => h(App),
});
```

在组件内提交 `mutations`:

```js
// 获取当前 count 值
console.log(this.$store.state.count); // 0

// 加 1
this.$store.commit('add');
console.log(this.$store.state.count); // 1

// 减 1
this.$store.commit('minus');
console.log(this.$store.state.count); // 0
```

使用 `computed` 属性:

```js
computed: {
	count() {
		return this.$store.state.count;
	}
}
```
