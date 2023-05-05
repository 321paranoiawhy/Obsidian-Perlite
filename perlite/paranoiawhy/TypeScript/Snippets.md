# Object is possibly 'null'.

```ts
const element = document.querySelector<HTMLElement>('.element');
// 1. if
if(element !== null) {
	element.style.color = 'red';
}

// 2. TS !. 非空断言
element!.style.color = 'red';

// 3. &&
element && (element!.style.color = 'red');
```

# setInterval Type

- [What's the Return Type for setTimeout() in Typescript](https://bobbyhadz.com/blog/typescript-settimeout-type)
- [setInterval - Type 'Timer' is not assignable to type 'number' #1053](https://github.com/TypeStrong/atom-typescript/issues/1053)

- 直接调用 `setInterval` 其返回类型为 `NodeJS.Timer`, [源码](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/010a8de/types/node/timers.d.ts#L73-L76)
- 调用 `window.setInterval` 其返回类型为 `number`, 但会在服务端渲染 `SSR (Server Side Render)` 出现问题

```ts
import { setInterval, clearInterval } from 'timers';

// 自动推断为 NodeJS.Timer
const nodeInterval = setInterval(() => {
  // do something
}, 1000);

clearInterval(nodeInterval);
```

```ts
const windowInterval: number = window.setInterval(() => {
  // do something
}, 1000);

clearInterval(windowInterval);
```

或者使用 `ReturnType` 和 `typeof`:

```ts
const nodeInterval: ReturnType<typeof setInterval> = setInterval(() => {
  // do something
}, 1000);
```

> [!tip] Go to Type Definition
> 在 `VS Code` 中右键 `setInterval` 选择 `Go to Type Definition` 即可跳转至类型定义源文件。
