# 下载和引入

```bash
dart pub add easy_debounce

flutter pub add easy_debounce
```

或者直接在 `pubsppec.yaml` 中添加依赖:

```yaml
dependencies:
  easy_debounce: ^2.0.3
```

引入:

```dart
import 'package:easy_debounce/easy_debounce.dart';
```

# 使用

## 防抖

> [!tip]
> 防抖指固定时间内最多执行一次, 如设置防抖时间为 `2s`, 则 `2s` 内重复操作最终只会以最后一次操作为准, 并在最后一次操作的 `2s` 后执行, 最后一次操作之前的所有操作均被略过。

```dart
EasyDebounce.debounce(
    'my-debouncer',                 // <-- An ID for this particular debouncer
    Duration(milliseconds: 500),    // <-- The debounce duration
    () => myMethod()                // <-- The target method
);
```

手动执行防抖:

```dart
EasyDebounce.fire('my-debouncer');
```

取消防抖:

```dart
// 取消特定的防抖
EasyDebounce.cancel('my-debouncer');

// 取消所有已设置的防抖和节流
EasyDebounce.cancelAll();
```

## 节流

> [!tip]
> 节流指固定时间内只执行一次, 重复的操作按顺序执行。节流可防止固定时间内频繁请求等(控制执行/请求频率)。

```dart
EasyThrottle.throttle(
    'my-throttler',                 // <-- An ID for this particular throttler
    Duration(milliseconds: 500),    // <-- The throttle duration
    () => myMethod()                // <-- The target method
    onAfter: (){ ... }              // <-- Optional callback, called after the duration has passed 
);
```

手动执行节流:

```dart
EasyDebounce.fire('my-throttler');
```

取消节流:

```dart
// 取消特定的节流
EasyDebounce.cancel('my-throttler');

// 取消所有已设置的防抖和节流
EasyDebounce.cancelAll();
```

## 获取已有数量

```dart
EasyThrottle.count();
```

# JavaScript 实现防抖和节流

防抖:

```js
const debounce = (fn, delay) => {
  let timer;
  return function () {
    // 清除上一次的定时器
    timer && clearTimeout(timer);

    // 新的定时器
    timer = setTimeout(() => {
      fn.apply(this, arguments);
    }, delay);
  };
};

debounce(() => {
  console.log("debounce");
}, 2000)();
```

- [debounce - lodash](https://lodash.com/docs/4.17.15#debounce)
- [debounce - underscore](https://underscorejs.org/#debounce)

节流(时间戳):

```js
const throttle = (fn, delay) => {
  let previousTime = 0;

  return function (...args) {
    if (new Date() - previousTime > delay) {
      previousTime = new Date();
      fn.apply(this, args);
    }
  };
};
```

使用时间戳虽然能实现节流, 但是最后一次事件不会执行。

节流(定时器):

```js
const throttle = (fn, delay) => {
  let timer;

  return function () {
    if (!timer) {
      timer = setTimeout(() => {
        timer = null;
        fn.apply(this, arguments);
      }, delay);
    }
  };
};
```

使用定时器实现节流, 虽然最后一次能触发, 但是第一次不会触发。

节流:

```js
const throttle = (fn, delay) => {
  let previousTime = 0,
    timer;

  return function () {
    if (new Date() - previousTime > delay) {
      clearTimeout(timer);
      timer = null;
      previousTime = new Date();
      fn.apply(this, arguments);
    } else {
      timer = setTimeout(() => {
        fn.apply(this, arguments);
      }, delay);
    }
  };
};
```

- [throttle - lodash](https://lodash.com/docs/4.17.15#throttle)
- [throttle - underscore](https://underscorejs.org/#throttle)


节流使用场景:

```js
// 滚动窗口
window.addEventListener('scroll', throttle(onScroll, 200));

// input 搜索
throttle(onInputSearch, 300);
```

- [Debouncing and Throttling Explained Through Examples - CSS-TRICKS](https://css-tricks.com/debouncing-throttling-explained-examples/)