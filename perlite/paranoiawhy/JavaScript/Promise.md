# Promise Concurrency

- [Promise Concurrency - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#promise_concurrency)

## Promise.all

- [Promise.all - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)
- `Promise.all` 为并发请求
- 所有请求都成功, 按顺序返回各请求结果数组
- 有一个请求失败, 返回失败原因, 并直接中断, 不再继续请求

所有请求都成功:

```js
const delay = function delay(time) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(time);
    }, time);
  });
};

const tasks = [delay(1000), delay(2000), delay(3000), delay(4000)];

console.time("总耗时");
const run = async (tasks) => {
  const result = await Promise.all(tasks);
  console.log("result: ", result); // result:  [ 1000, 2000, 3000, 4000 ]
  console.timeEnd("总耗时"); // 总耗时: 4.017s
};
run(tasks);
```

上述四个任务分别耗时 `1000ms`、`2000ms`、`3000ms` 和 `4000ms` , `Promise.all` 总耗时 `4.017s` , 约等于最长任务耗时 ---**长板效应**。

有一个请求失败:

```js
const promise1 = Promise.resolve(1);
const promise2 = Promise.reject(2);
const promise3 = Promise.resolve(3);

const tasks = [promise1, promise2, promise3];

Promise.all(tasks).then((results) =>
  results.forEach((result) => console.log(result))
);
// Expected output:
// Uncaught (in promise) 2
```

## Promise.allSettled

- [Promise.allSettled - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled)
- 无论请求成功还是失败, `Promise.allSettled` 都会等待所有请求结束再返回结果
- 返回一个对象数组结果, 每个对象上均有 `status` 属性, 其值为字符串
- `status` 属性值为 `fulfilled` 或 `rejected`
- `status` 属性为 `fulfilled` 时, 该对象上还有 `value` 属性
- `status` 属性为 `rejected` 时, 该对象上还有 `reason` 属性

```js
const promise1 = Promise.resolve(1);
const promise2 = Promise.reject(2);
const promise3 = Promise.resolve(3);

const tasks = [promise1, promise2, promise3];

Promise.allSettled(tasks).then((results) => console.log(results));

// Expected output:
// [
//   { status: 'fulfilled', value: 1 },
//   { status: 'rejected', reason: 2 },
//   { status: 'fulfilled', value: 3 } 
// ]
```

## Promise.any

- [Promise.any](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any)
- 只要有一个请求成功, 即返回该请求结果

```js
const promise1 = Promise.resolve(1);
const promise2 = Promise.reject(2);
const promise3 = Promise.resolve(3);

const tasks = [promise1, promise2, promise3];

Promise.any(tasks).then((result) => console.log(result));
// Expected output:
// 1
```

> [!attention]
> `Node.js` 版本必须大于 `15.0.0` , 否则不支持 Promise.any
> - [Getting error TypeError: Promise.any is not a function - Stackoverflow](https://stackoverflow.com/questions/63123579/getting-error-typeerror-promise-any-is-not-a-function)
> - [Implement Promise.any - node issue](https://github.com/nodejs/node/issues/35045)
> - [node.js v15](https://github.com/nodejs/node/pull/34337#issuecomment-700711371)

## Promise.race

- [Promise.race](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)
- 返回最快请求的结果

```js
const delay = function delay(time) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(time);
    }, time);
  });
};

const tasks = [delay(3000), delay(2000), delay(1000), delay(4000)];

Promise.race(tasks).then((result) => console.log(result));
// Expected output:
// 1000
```

# 中断请求

- [AbortController - MDN](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)