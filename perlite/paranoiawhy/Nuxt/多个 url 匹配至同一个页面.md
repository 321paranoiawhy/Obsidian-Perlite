页面文件目录 `pages/example/entry.vue`
可匹配的 `url`:

- `/example/entryA`
- `/example/entryB`

```vue
definePageMeta({
  // /example/entry
  alias: ['/example/entryA', '/example/entryB'],
})
```