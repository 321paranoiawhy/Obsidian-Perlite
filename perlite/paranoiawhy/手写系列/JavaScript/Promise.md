## Promise.all

### 特点

- 接收一个[可迭代对象或类数组对象](https://zh.javascript.info/iterable#array-like)
- 并行执行, 运行时间取决于最慢的 `Promise`
- 输出一个 `Promise` 对象
- 输入和输出的顺序保持一致
- 只要有任意一个 `Promise` 失败即 `reject`
- 所有 `Promise` 都成功才 `resolve`

```ts
type HWPromise = {
  all: Function;
};

const HWPromise: HWPromise = { all: () => {} };

HWPromise.all = (
  iterable: Iterable<Promise<any>> | ArrayLike<Promise<any>>
): Promise<any> => {
  return new Promise((resolve, reject) => {
    const promises = Array.from(iterable);
    const result: Promise<any>[] = [];
    let count = 0;
    for (let i = 0; i < promises.length; i++) {
      Promise.resolve(promises[i])
        .then((res) => {
          result[i] = res;
          count++;
          if (count === promises.length) {
            resolve(result);
          }
        })
        .catch((err) => reject(err));
    }
  });
};
```

示例:

```ts
(async () => {
  const res = await HWPromise.all([1, 2, 3]);
  console.log(res);
})();
```

```ts
const delay = function delay(time: number): Promise<number> {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(time);
    }, time);
  });
};

const tasks = [delay(1000), delay(2000), delay(3000), delay(4000)];

console.time("总耗时");
const run = async (tasks: Iterable<Promise<any>> | ArrayLike<Promise<any>>) => {
  const result = await HWPromise.all(tasks);
  console.log("result: ", result); // result:  [ 1000, 2000, 3000, 4000 ]
  console.timeEnd("总耗时"); // 总耗时: 4.000s
};
run(tasks);
```

## Promise.any

```ts
type HWPromise = {
  any: Function;
};

const HWPromise: HWPromise = { any: () => {} };

HWPromise.any = (
  iterable: Iterable<Promise<any>> | ArrayLike<Promise<any>>
): Promise<any> => {
  return new Promise((resolve, reject) => {
    const promises = Array.from(iterable);
    for (let i = 0; i < promises.length; i++) {
      Promise.resolve(promises[i])
        .then((res) => {
          resolve(res);
        })
        .catch((err) => reject(err));
    }
  });
};
```

示例:

```ts
const promise1 = Promise.resolve(1);
const promise2 = Promise.reject(2);
const promise3 = Promise.resolve(3);

const tasks = [promise1, promise2, promise3];

HWPromise.any(tasks).then((result: any) => console.log(result)); // 1
```