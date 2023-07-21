# 对象类型

可以使用 `interface` 或 `type`:

```ts
interface Person {
  name: string;
  age: number;
}
```

上述类型一定程度上等价于:

```ts
type Person = {
  name: string;
  age: number;
};
```

注意用 `type` 定义相较于 `interface` 定义花括号前多了个等于号 **=**。

## 可选属性

- [Optional Properties](https://www.typescriptlang.org/docs/handbook/2/objects.html#optional-properties)

```ts
interface User {
  username?: string; // username 为可选属性
  email: string;
}
```

在使用可选属性时须检查其是否存在:

```ts
const findUserBy = (user: User): User => {
  return typeof user.username === "undefined"
    ? { email: user.email }
    : { username: user.username, email: user.email };
};
```

当然也可以使用如下方式检查:

```ts
user.username === undefined
```

[How can I check for "undefined" in JavaScript?](https://stackoverflow.com/a/3390635)

## 只读属性

- [`readonly` Properties](https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties)

```ts
interface readonlyProperty {
  readonly prop: string;
}

const readonlyProperty: readonlyProperty = {
  prop: "prop",
};

// OK: 读取属性
console.log(readonlyProperty.prop); // "prop"

// Error: Cannot assign to 'prop' because it is a read-only property.
readonlyProperty.prop = "new prop";
```

关于不可变:

- [immutable-js](https://immutable-js.com/)
- [Immer](https://immerjs.github.io/immer/)

## 去除可选属性或只读属性

### 将所有可选属性都变为必须属性:

```ts
// 含 username 可选属性
type UserWithOptionalUsername = {
  username?: string;
  email: string;
};

// 去除所有可选属性
type RemoveAllOptionalKeys<T> = {
  [key in keyof T]-?: T[key];
};

// username 由可选属性变为必须属性
type UserWithoutOptionalUsername =
  RemoveAllOptionalKeys<UserWithOptionalUsername>;
// type UserWithoutOptionalUsername = {
//   username: string;
//   email: string;
// };
```

`RemoveAllOptionalKeys` 正是 [Required](https://www.typescriptlang.org/docs/handbook/utility-types.html#requiredtype) 的实现:

```ts
type Required<T> = {
  [P in keyof T]-?: T[P];
};
```

### 将所有只读属性都变为可变属性:

```ts
// 含 username 只读属性
type UserWithReadonlyUsername = {
  readonly username: string;
  email: string;
};

// 去除所有只读属性
type RemoveAllReadonlyKeys<T> = {
  -readonly [key in keyof T]: T[key];
};

// username 由只读属性变为可变属性
type UserWithoutReadonlyUsername =
  RemoveAllReadonlyKeys<UserWithReadonlyUsername>;

// type UserWithoutReadonlyUsername = {
//   username: string;
//   email: string;
// };
```

上述代码中 `RemoveAllReadonlyKeys` 可重命名为 `Mutable`:

```ts
type Mutable<T> = {
  -readonly [P in keyof T]: T[P];
};
```

### 将所有属性都变为只读属性:

```ts
type _Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

// 含有 name 和 age 两个属性
type User = {
  name: string;
  age: number;
};

// name 和 age 两个属性为只读属性
type UserAllKeysAreReadonly = _Readonly<User>;
```

上述代码正是 [Readonly](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype) 的实现。

### 将所有属性都变为可选属性:

```ts
type _Partial<T> = {
  [P in keyof T]?: T[P] | undefined;
};

// 含有 name 和 age 两个必须属性
type User = {
  name: string;
  age: number;
};

// name 和 age 两个属性为可选属性
type UserAllKeysAreOptional = _Partial<User>;
```

上述代码正是 [Partial](https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype) 的实现。

### 取出部分属性:

```ts
type _Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

// 含有 name 和 age 两个属性
type User = {
  name: string;
  age: number;
};

// 仅含有 name 属性的 User
type UserOnlyHaveName = _Pick<User, "name">;
```

上述代码正是 [Pick](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys) 的实现。

## 扩展类型

- [Extending Types](https://www.typescriptlang.org/docs/handbook/2/objects.html#extending-types)

扩展类型将拥有被扩展类型的所有特性, 可**新增特性**或**维持原特性**。

```ts
interface User {
  name: string;
}

// 新增 age 键, 其值的类型为字符串
interface UserWithAge extends User {
  age: string;
}

// 维持原特性, 保持不变
interface AnotherUser extends User {}
```

多继承(扩展):

```ts
interface User {
  name: string;
}

interface UserWithAge extends User {
  age: string;
}

interface UserWithAgeAndSex extends User, UserWithAge {
  sex: string;
}
```

## 并集

- [Intersection Types](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types)
- [Interfaces vs. Intersections](https://www.typescriptlang.org/docs/handbook/2/objects.html#interfaces-vs-intersections)

```ts
interface Colorful {
  color: string;
}
interface Circle {
  radius: number;
}

type ColorfulCircle = Colorful & Circle;
```

也可以使用 `extends` 实现同样的效果:

```ts
interface ColorfulCircle extends Colorful, Circle {}
```

# 数组类型

- [The `Array` Type](https://www.typescriptlang.org/docs/handbook/2/objects.html#the-array-type)

> [!tip]
> `Array<T>` 等价于 `T[]`, 后者为前者的简写语法。

字符串数组:

```ts
const arr1: Array<string> = ['1'];
const arr2: string[] = ['1'];
```

只读数组:

```ts
const readonlyArray: ReadonlyArray<string> = ['1'];
const readonlyArray2: readonly string[] = ['1'];
```

# 元组类型

- [Tuple Types](https://www.typescriptlang.org/docs/handbook/2/objects.html#tuple-types)

```ts
type fixedArray = [string, number];

// OK
const arr: fixedArray = ['0', 1];
```

指定类型为 `fixedArray` 后, 其索引 `0` 处的元素必须是 `string`, 索引 `1` 处的元素必须是 `number`, 且数组的长度是固定的 (`2`)。

元组中也可以有可选元素:

```ts
type tupleWithOptionalElement = [string, number?];

// OK
const arr1:tupleWithOptionalElement = ['0'];
// OK
const arr2:tupleWithOptionalElement = ['0', 1];
```

只读元组:

```ts
const readonlyTuple: readonly [string, number] = ["0", 1];
// Cannot assign to '0' because it is a read-only property.
readonlyTuple[0] = '1';
```

> [!danger]
> 无法对元组中部分元素限定只读:
> 
> ```ts
> // 索引 1 处的元素只读
> // 'readonly' type modifier is only permitted on array and tuple literal types.
> const readonlyElementAtIndexOne: [string, readonly number] = ["1", 1];
> ```

使用 `as const` 类型断言将数组转换为只读元组:

```ts
const point = [1, 2] as const;

// 等价于
const point: readonly [number, number] = [3, 4];
```
