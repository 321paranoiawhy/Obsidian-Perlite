# 获取单个 `DOM` 元素

`template` 元素挂上 `ref="refName"`:

```html
<div ref="divRef"></div>
```

## `Vue 2`

在 `script` 中使用 `this.$refs.refName` 获取 `DOM` 元素:

```js
this.$refs.divRef;
```

> [!hint]
> `refName` 指 `ref` 属性的值。

```

## `Vue 3` 非顶层 `setup`

```js
<script>
import { ref, onMounted } from "vue";

export default {
	name:"example",
	setup(props, context){
		const divRef = ref(null);
		
		console.log(divRef.value); // undefined, 因此时 DOM 元素未渲染
		
		// onMounted 里可以正常拿到 DOM 元素的引用
		onMounted(()=>{
			console.log(divRef.value);
		});
		// divRef 需要 return 出去
		return {
			divRef,
		};
	},
}
</script>
```

## `Vue 3` 顶层 `setup`

```js
<script setup lang="ts">
import { ref, onMounted } from "vue";

const divRef = ref();

console.log(divRef.value); // undefined, 因此时 DOM 元素未渲染

// onMounted 里可以正常拿到 DOM 元素的引用
onMounted(()=>{
	console.log(divRef.value);
});
</script>
```

## Reference

[Template Refs](https://vuejs.org/guide/essentials/template-refs.html)

# 获取多个 `DOM` 元素

`template`:

```html
<div v-for="(item, index) in listData" ref="divRef"></div>
```

## `Vue 2`

[Refs inside `v-for`](https://vuejs.org/guide/essentials/template-refs.html#refs-inside-v-for)

```js
<script>
export default {
  data() {
    return {
      listData: [1, 2, 3],
    };
  },
  mounted() {
    console.log(this.$refs.divRef);
    this.$refs.divRef.forEach((item) => {
	    console.log(item);
    });
  }
}
</script>
```

## `Vue 3` 非顶层 `setup`

```js
<script>
import { ref, onMounted } from "vue";

export default {
	name: "example",
	setup(props, context){
		const divRef = ref(null);
		
		// onMounted 里可以正常拿到 DOM 元素的引用
		onMounted(()=>{
			console.log(divRef.value);
			divRef.value.forEach((item) => {
		    console.log(item);
		    });
		});
		// divRef 需要 return 出去
		return {
			divRef,
		};
	},
}
</script>
```

## `Vue 3` 顶层 `setup`

```js
<script setup lang="ts">
import { ref, onMounted } from "vue";

const divRef = ref(null);

// onMounted 里可以正常拿到 DOM 元素的引用
onMounted(()=>{
	console.log(divRef.value);
	divRef.value.forEach((item) => {
	    console.log(item);
    });
});
</script>
```

# 获取组件实例

```html
<Child ref="child"></Child>
```

## `Vue 2`

```js
this.$refs.child;
```

## `Vue 3` 非顶层 `setup`

```js
<script>
import { ref, onMounted } from "vue";
import Child from "./Child.vue";

export default {
	name: "example",
	components:{
		Child,
	},
	setup(props, context){
		const child = ref(null);
		onMounted(()=>{
			console.log(child.value);
		});
		return {
			child,
		};
	},
}
</script>
```

## `Vue 3` 顶层 `setup`

```js
<script setup lang="ts">
import { ref, onMounted } from "vue";
import Child from "./Child.vue";

const child = ref(null);
onMounted(() => {
	console.log(child.value);
});
</script>
```

# `调用子组件方法`

```js
childComponent.method();
```

> [!TIP]
>  - `childComponent` 表示 `this.$refs.child` 或 `child.value`;
>  - `method` 表示 `childComponent` 的一个方法。

# `改变子组件状态`

```js
childComponent.state = newState;
```

> [!tip]
> - `childComponent` 表示 `this.$refs.child` 或 `child.value`;
> - `state` 表示 `childComponent` 的一个状态变量。