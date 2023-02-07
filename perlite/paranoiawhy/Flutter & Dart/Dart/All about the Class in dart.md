# `Object`

* 超级父类 `Object`: 所有 `类` 都直接或间接继承自 `Object`;
* 一切皆对象;

# 获取对象类型

```dart
List list = [];
list.runtimeType; // List<dynamic>
```

# Callable Class

[Callable classes - dart.dev](https://dart.dev/guides/language/language-tour#callable-classes)

Implement `call()` method:

```dart
class CallableClass {
	String call(String a, String b, String c) => "$a $b $c!";
}

void main() => print(CallableClass()("Hi", "there", "dart"));
```