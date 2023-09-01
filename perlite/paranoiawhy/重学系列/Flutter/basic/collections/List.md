# 构造

## 字面量

使用方括号(`[` 和 `]`)包裹即可创建一个数组:

```dart
List list = [];
```

## `List.from`

- [List\<E>.from constructor](https://api.flutter.dev/flutter/dart-core/List/List.from.html)

```dart
List<int> list = [1, 2, 3];

final listFrom = List<int>.from(list);
print(listFrom); // [1, 2, 3]
```

`List.from` 不会自动推断类型(`downcast`), 其类型为 `List<dynamic>`:

```dart
final foo = List.from(<int>[1, 2, 3]); // List<dynamic>
```

## `List.of`

- [List\<E>.of constructor](https://api.flutter.dev/flutter/dart-core/List/List.of.html)

```dart
List<int> numbers = [1, 2, 3];

final listOf = List<num>.of(numbers);
print(listOf); // [1, 2, 3]
```

`List.of` 可自动推断类型, 是类型安全的:

```dart
final bar = List.of(<int>[1, 2, 3]); // List<int>
```

## `List.generate`

- [List\<E>.generate constructor](https://api.flutter.dev/flutter/dart-core/List/List.generate.html)

传入 `growable` 为 `true`, 则数组长度可变:

```dart
final growableList =
    List<int>.generate(3, (int index) => index * index, growable: true);

print(growableList); // [0, 1, 4]
```

传入 `growable` 为 `false`, 则数组长度不可变:

```dart
final fixedLengthList =
    List<int>.generate(3, (int index) => index * index, growable: false);

print(fixedLengthList); // [0, 1, 4]

fixedLengthList.add(9); // Error
```

## `List.empty`

- [List\<E>.empty constructor](https://api.flutter.dev/flutter/dart-core/List/List.empty.html)

`List.empty` 语法自 `2.9` 引入。

```dart
final growableList = List.empty(growable: true); // []
growableList.add(1); // [1]

final fixedLengthList = List.empty(growable: false);
fixedLengthList.add(1); // Error
```

# 插入元素

## `add`

向数组末尾插入单个元素:

```dart
List list = [];

list.add(1);
list.add(2);
list.add(3);

print(list); // [1, 2, 3]
```

注意, 必须为 `growable` 数组:

```dart
final numbers = <int>[1, 2, 3];

final unmodifiableList = List.unmodifiable(numbers); // [1, 2, 3]

unmodifiableList.add(4); // Error

unmodifiableList[0] = 0; // Error
```

使用 `List.unmodifiable` 构造的数组, 长度和元素都不可变, 可理解为不可变数组(元组)。

# 移除数组元素

# 清空数组

就地清空, 引用不变:

```dart
List list = [1, 2, 3];

list.clear();
```

非就地清空, 替换为新的引用:

```dart
List list = [1, 2, 3];

list = [];
```

如果数组被声明为 `final` 或 `const`, 则无法更改引用:

```dart
final List list = [1, 2, 3];

list = []; // Error
```

# 合并数组

`+` 操作符:

```dart
List list1 = [1, 2, 3];
List list2 = [4, 5, 6];

print(list1 + list2); // [1, 2, 3, 4, 5, 6]
```

[源码](https://github.com/dart-lang/sdk/blob/main/sdk/lib/collection/list.dart#L345)实现如下:

```dart
List<E> operator +(List<E> other) => [...this, ...other];
```

可以看到 `+` 操作符实际上是 `...` 扩展运算符合并数组的语法糖, 因此等价于:

```dart
List list1 = [1, 2, 3];
List list2 = [4, 5, 6];

print([...list1, ...list2]); // [1, 2, 3, 4, 5, 6]
```

# 数组排序

- [sort abstract method](https://api.flutter.dev/flutter/dart-core/List/sort.html)

```dart
List list = [1, 3, 2];

print(list.sort()); // [1, 2, 3]

// 按数字大小升序排列
print(list.sort((a, b) => a.compareTo(b))); // [1, 2, 3]

// 按数字大小降序排列
print(list.sort((a, b) => b.compareTo(a))); // [3, 2, 1]
```

如果未传比较函数, 则使用默认的 [Comparable.compare](https://api.flutter.dev/flutter/dart-core/Comparable/compare.html)比较函数进行排序:

```dart
List<int> list = [13, 2, -11, 0];

print(list.sort()); // [-11, 0, 2, 13]
```

# 打乱数组

- [shuffle abstract method](https://api.flutter.dev/flutter/dart-core/List/shuffle.html)

[源码](https://github.com/dart-lang/sdk/blob/main/sdk/lib/collection/list.dart#L328-L339)实现:

```dart
void shuffle(List elements, [int start = 0, int? end, Random? random]) {
  random ??= Random();
  end ??= elements.length;
  var length = end - start;
  while (length > 1) {
    var pos = random.nextInt(length);
    length--;
    var tmp1 = elements[start + pos];
    elements[start + pos] = elements[start + length];
    elements[start + length] = tmp1;
  }
}
```

```dart
List<int> list = [1, 2, 3, 4];

print(list.shuffle()); // maybe: [3, 1, 2, 4]
```

# 浅复制和深复制数组

# 转换为其他类型

## `toString`

- [toString](https://api.flutter.dev/flutter/dart-core/Object/toString.html)

## `toSet`

- [toSet method](https://api.flutter.dev/flutter/dart-core/Iterable/toSet.html)

```dart
List list = [1, 1, 2, 3, 3, 4];

print(list.toSet()); // {1, 2, 3, 4}

// 或者解构 list
print({...list}); // {1, 2, 3, 4}
```

## `asMap`

- [asMap abstract method](https://api.flutter.dev/flutter/dart-core/List/asMap.html)

## `cast`

- [cast\<R> abstract method](https://api.flutter.dev/flutter/dart-core/List/cast.html)
