# print

```dart
print(‘This is a print.);
```

> [!tip]
> Avoid `print` calls in production code. dart(avoid_print)

# debugPrint

```dart
debugPrint('This is a debug print.');
```

# developer.log

`developer.log` 可以定制更精细化的消息打印。

```dart
import 'dart:developer' as developer;

developer.log('This is a developer log.');
```

# 生产环境下禁止打印

- [Flutter/Dart Release 模式下屏蔽 debugPrint 与 Print 输出](https://droidyue.com/blog/2022/05/23/disable-debugprint-and-print-in-flutter-dart-release-mode/)

## debugPrint

- `kReleaseMode`: release builds [kReleaseMode](https://api.flutter.dev/flutter/foundation/kReleaseMode-constant.html)
- `kProfileMode`: profile builds [kProfileMode](https://api.flutter.dev/flutter/foundation/kProfileMode-constant.html)
- `kDebugMode`: debug builds [kDebugMode](https://api.flutter.dev/flutter/foundation/kDebugMode-constant.html)

`debugPrint` 表面上看只会在 `debug` 模式下打印消息, 但实际上它在 `release` 模式下也会打印消息, 但可以通过如下方式在 `release` 模式下禁用其打印:

```dart
import 'package:flutter/foundation.dart';

if(kReleaseMode) {
   debugPrint = (String? message, {int? wrapWidth}) {
     // empty debugPrint implementation in the release mode
    };
}
```

> [!important]
> 上述代码须在 `runApp(const MyApp())` 之前运行。

`kDebugMode` 的实现:

```dart
const bool kDebugMode = !kReleaseMode && !kProfileMode;
```

## print