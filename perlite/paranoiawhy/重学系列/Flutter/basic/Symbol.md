# 创建

有两种方式创建 `Symbol`:

- `#` 前缀
- `Symbol` 构造函数

```dart
final Symbol symbol1 = #symbol;

final Symbol symbol2 = Symbol('symbol');
```

每个 `Symbol` 都是独一无二的, 彼此互不相等, 即使传入值相同:

```dart
final Symbol symbol1 = Symbol('symbol');
final Symbol symbol2 = Symbol('symbol');

print(symbol1 == symbol2);
```
