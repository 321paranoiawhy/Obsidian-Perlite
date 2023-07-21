## 高度

```dart
@override
BoxConstraints getConstraintsForChild(BoxConstraints constraints) {
  return BoxConstraints(
    minWidth: constraints.maxWidth,
    maxWidth: constraints.maxWidth,
    maxHeight: isScrollControlled
        ? constraints.maxHeight
        : constraints.maxHeight * 9.0 / 16.0,
  );
}
```

当 `isScrollControlled` 为 `true` 时, `maxHeight` 为 `constraints.maxHeight`, 表示不限制高度, `showModalBottomSheet` 默认高度为全屏;

当 `isScrollControlled` 为 `false` 时, `maxHeight` 为 `constraints.maxHeight * 9.0 / 16.0`, 限制最大高度为屏幕高度的 **9 / 16**。

那么如何在 `isScrollControlled` 为 `false` 时自定义最大高度呢?

一种方式是拷贝源码, 手动修改所有未带上 `package:flutter` 的引入内容

```dart
import 'colors.dart';
```

改为:

```dart
import 'package:flutter/src/material/colors.dart';
```

同时修改原有的 `showModalBottomSheet` 为 `showCustomModalBottomSheet`, 并添加 `heightRatio` 参数:

```dart
final double progress;
final bool isScrollControlled;

final double heightRatio;

@override
BoxConstraints getConstraintsForChild(BoxConstraints constraints) {
  return BoxConstraints(
    minWidth: constraints.maxWidth,
    maxWidth: constraints.maxWidth,
    maxHeight: isScrollControlled
        ? constraints.maxHeight
        : constraints.maxHeight * heightRatio,
  );
}
```
