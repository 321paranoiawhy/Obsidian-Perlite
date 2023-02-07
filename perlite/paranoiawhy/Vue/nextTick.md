#nextTick #Vue
#  `Vue 2`

```js
this.$nextTick(()=>{
	// do something
});
```

- [$nextTick() - vue 2](https://vuejs.org/api/component-instance.html#nexttick)

# `Vue 3`

```js
import { nextTick } from "vue";

const handleNextTick = async () => {
	await nextTick();
	// do something
}
```

- [nextTick() - vue 3](https://vuejs.org/api/general.html#nexttick)