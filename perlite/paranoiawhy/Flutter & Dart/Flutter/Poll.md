#Poll #轮询
# 轮询

- [Timer.periodic constructor](https://api.flutter.dev/flutter/dart-async/Timer/Timer.periodic.html)

# 固定次数

```dart
/// duration 轮询间隔时间 (默认值 1s)
/// maxCount 最大轮询次数 (默认值 10)
/// callback 须执行的回调函数
void poll(
    {Duration duration = const Duration(seconds: 1),
    int maxCount = 10,
    required Function callback}) {
  int currentCount = 1;
  Timer.periodic(duration, (timer) {
    if (currentCount <= maxCount) {
	    callback(currentCount);
      currentCount++;
    } else {
      timer.cancel();
    }
  });
}

poll(callback: (currentCount) => print(currentCount));
```

# 固定条件

## `dart_eval`

```dart
import 'package:dart_eval/dart_eval.dart';

void poll(
    {Duration duration = const Duration(seconds: 1),
    required String condition,
    required Function callback}) {
  Timer.periodic(duration, (timer) {
    if (eval(condition)) {
      timer.cancel();
    }
  });
}

int a = 1;
poll(
    condition: "a == 5",
    callback: () {
      print(a);
      a++;
    });
```

## `Isolate`

```dart
import 'dart:isolate';

void main() async {
  final uri = Uri.dataFromString(
    '''
    void main() {
      print("Hellooooooo from the other side!");
    }
    ''',
    mimeType: 'application/dart',
  );
  await Isolate.spawnUri(uri, [], null);
}
```

## Reference

- [dart_eval - GitHub](https://github.com/ethanblake4/dart_eval)
- [dart_eval - pub.dev](https://pub.dev/packages/dart_eval)
- [how-do-i-execute-dynamically-like-eval-in-dart - stcakoverflow](https://stackoverflow.com/questions/13585082/how-do-i-execute-dynamically-like-eval-in-dart)
- [Running arbitrary strings as Dart code - iiro.dev](https://iiro.dev/how-to-eval-in-dart/)
