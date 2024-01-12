- [clickoutside.js](https://github.com/ElemeFE/element/blob/dev/src/utils/clickoutside.js)
- [onClickOutside](https://vueuse.org/core/onClickOutside/)
- [clickoutside.js 源码解析](https://blog.tianyichuxin.com/2021/08/38262.html)

使用方式:

1. 引入:

```vue
import Clickoutside from 'element-ui/lib/utils/clickoutside'
```

2. 声明指令:

```vue
export default {
	directives: { Clickoutside },
}
```

3. 在模板中使用:

```vue
<!-- onClickOutside 为处理函数 -->
<div v-clickoutside="onClickOutside"></div>
<div v-clickoutside="() => showTooltip = false"></div>
```