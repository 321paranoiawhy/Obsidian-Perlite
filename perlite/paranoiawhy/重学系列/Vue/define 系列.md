# defineProps

- [Typing Component Props](https://vuejs.org/guide/typescript/composition-api.html#typing-component-props)

类 `Vue2` props 类型写法:

```vue
<script setup lang="ts">
const props = defineProps({
  foo: { type: String, required: true },
  bar: Number
})

props.foo // string
props.bar // number | undefined
</script>
```

指定泛型:

```vue
<script setup lang="ts">
const props = defineProps<{
  foo: string
  bar?: number
}>()
</script>
```

或者指定 `type` 或 `interface`:

```vue
<script setup lang="ts">
interface Props {
  foo: string
  bar?: number
}

const props = defineProps<Props>()
</script>
```

设置默认值:

```vue
<script setup lang="ts">
export interface Props {
  msg?: string
  labels?: string[]
}

const props = withDefaults(defineProps<Props>(), {
  msg: 'hello',
  labels: () => ['one', 'two']
})
</script>
```

# defineExpose